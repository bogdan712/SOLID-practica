# Principios SOLID

He modificado el getSize de la clase **Directory.java** para que devuelva el tamaño total de los ficheros y directorios que contiene, puesto en mi primer commit:
```
commit  = 2a21dcfd4297a1c05056308433ae3d75c2b838e6
```
Este es el código del commit anterior:
```java
@Override
    public int getSize() {
        public int getSize() {
            int size = 0;
            for (FileSystemItem item : files) {
                size += item.getSize();
            }
            System.out.println("El tamaño total de los archivos y directorios en " + getName() + " es " + size);
            return size;
        }
    }
```
He detectado que en algunas clases se están incumpliendo algunos de los principios SOLID, por lo tanto, voy a explicar donde los he detectado con el principio que están incumpliendo haciendo una justificación del porqué lo incumplen.

# Principios Incumplidos :

## Principio de Segregación de la Interfaz :


De acuerdo con el principio, al definir interfaces deben de tener una finalidad en concreto y es mejor hacer muchas interfaces pequeñas que una muy grande, así evitamos métodos no necesarios. 

En este caso tenemos una interfaz llamada **FileSystemItem** que es muy grande con métodos que no son aplicables a todas las clases que la implementan. Por ejemplo, el método *"setParent"* entre otros, solamente se está aplicando en una sola clase , por lo que la implementación de este método es inútil en una de las clases, así violando el **principio de Segregación de la Interfaz**. 

La solución sería tener varias interfaces más especificas que cumplan algo en concreto y que a la hora de llamar a dicha interfaz haga exactamente lo que tiene que hacer, ni más ni menos.

## Principio de responsabilidad única :

Tanto la clase **Directory.java** como **File.java** son clase que están teniendo muchas responsabilidades, más conocidas como *“clases dios”* esto se puede considerar una violación del **principio de Responsabilidad Única**, ya que una clase debería tener una única razón para cambiar, además hay cierto código que se está repitiendo dentro de la misma clase.

Por lo tanto, una solución a esto, por ejemplo, sería dividir las responsabilidades de la clase **Directoriy.java** en varias clases más pequeñas y especializadas, podríamos tener una clase *"Lista de Archivos"* que solo sea responsable de mantener una lista de archivos, una clase *"Calculadora de Tamaño"* que solo calcule el tamaño total del directorio y una clase *"Gestor de Archivos"* que maneje la adición y eliminación de archivos y subdirectorios. En la otra clase haríamos lo mismo dividir la clase en responsabilidades más pequeñas.

## Principio de Inversión de Dependencias :

De acuerdo con el principio, los módulos de alto nivel no deben depender de los módulos de bajo nivel, sino que ambos deben depender de abstracciones.

En este caso, la clase **Directory.java** y **File.java** estén directamente acopladas a una implementación concreta de la interfaz **FileSystemItem**. Esto significa que si queremos cambiar la implementación concreta de FileSystemItem, será necesario modificar la clase Directory y File directamente, lo que rompe el **principio de Inversión de Dependencias**.

Por lo tanto, el uso de la inversión de dependencias en este caso permitiría desacoplar la clase **Directory.java** y **File.java** de una implementación concreta de **FileSystemItem**, permitiendo cambios de implementación en tiempo de ejecución sin tener que modificar la clase directamente. También permitiría la creación de pruebas de unidad más fáciles de mantener y extender, así como la extensión de la funcionalidad de la clase mediante la adición de nuevas implementaciones de FileSystemItem.

**Nota** He intentado aplicarlo al código, pero me daban muchos errores, después de estar varias horas intentándolo hacer he decidido volver a clonarlo el repositorio, ya que el código ya no compilaba, así poniendo que principio no se cumplía aunque no he podido resolverlo en forma de código.