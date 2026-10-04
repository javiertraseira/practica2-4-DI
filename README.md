# Práctica 2.5 Generador de números aleatorios

El objetivo de esta práctica es la de diseñar y desarrollar una aplicación gráfica que permita generar números aleatorios dentro de un rango definido por el usuario, aplicando los principios de separación de lógica en paquetes (Modelo y VistaControlador) y buenas prácticas de organización en proyectos Java. Además se aprenderá a crear pruebas automatizadas para testear apartados de la interfaz.

Crea un proyecto llamado *practica2-5* en la carpeta SOL de github. Utiliza *branches* para delimitar los cambios que vayas haciendo.

## Parte 1

Crear una interfaz mixta utilizando *FlatLaf* con los elementos indicados para un generador de números aleatorios gráfico. Utiliza el elemento *JSpinner* que mostrará el número aleatorio generado entre esos dos números en un campo *JTextField* al pulsar el botón generar.

La ventana deberá tener además un **menú** con los elementos Fichero y Edición. El menú fichero deberá tener por el momento un elemento salir y el menú *Edición* un elemento que permita reiniciar el contenido de los campos de la ventana.

Ayúdate de la función `Math.random()` entre dos números o de la clase `radom` así como de una **clase auxiliar** para realizar dichos cálculos.

```java
Math.random() * (max - min + 1) + (min)
```

```java
Random rnd = new Random();
rnd.nextDouble() * max + min

```

Verifica dónde se crea el fichero de empaquetado del proyecto `jar` al contruir el proyecto y ejecútalo desde la consola usando los comandos adecuados.

![](media/ba18dcfdd7fd2df3ed8dfe1cefa04f24.png)

## Parte 2

Divide el proyecto en dos paquetes diferenciados según su función: `VistaControlador` y `Modelo`
- Mejora el ejercicio anterior agregando un *checkbox* que en caso de estar marcado solo permita mostrar números **primos** entre los valores requeridos.
- Agrega en el *menú edición* los siguentes elementos: 

    - Una opción llamada **historial** que permita ver los últimos números generados en una ventana modal (*JDialog*) usando una lista (*JList*). Puedes editar la disposición de dicha ventana de diálogo desde el editor de Netbeans en la pestaña del *Navigator* en *Other Components*. 
    - Una opción para **guardar** el historial del listado generado en un fichero de texto mediante un *JFileChooser*. Se deberá verificar si ya existe un fichero con el mismo nombre antes de sobreescribirlo.
    - Otra última opción llamada *borrar todo* para eliminar el listado guardado del historial.  

- Busca la forma de forzar la creación del .jar al compilar (no solo al construir el proyecto).

## Pruebas (testing)

Crea el fichero de pruebas en la carpeta *TEST* del repositorio en un fichero llamado *resultado_pruebas.md*.

| ID Caso Prueba | Descripción Caso de Prueba                     | Entrada                                 | Salida Esperada                                                           | Resultado   |
|----------------|-----------------------------------------------|-----------------------------------------|---------------------------------------------------------------------------|-------------|
| 01             | Comprobación del botón "Generar"               | Escribir valores en mínimo y máximo     | Se genera un número aleatorio entre los valores indicados                  | OK/No cumple|
| 02             | Comprobación valores mínimo y máximo           | Escribir valores en mínimo y máximo     | Se comprueba que el rango mínimo sea menor que máximo                      | OK/No cumple|
| 03             | Comprobación checkbox "Sólo números primos"    | Escribir valores en mínimo y máximo     | Se comprueba que se generan números primos aleatorios entre los valores indicados | OK/No cumple|
| 04             | Comprobación del historial                     | Abrir ventana desde el menú edición > historial | Se muestra un historial de todos los valores mostrados en una lista `JList` | OK/No cumple|
| 05             | Comprobación guardado                          | Abrir desde el menú fichero > guardar   | Se muestra un `JFileChooser` para elegir dónde guardar un fichero con el historial de números generados | OK/No cumple|
| 06             | Comprobación duplicados                        | Abrir desde el menú fichero > guardar   | Se verifica que el fichero a guardar no exista ya, en cuyo caso pregunta si se desea sobrescribir | OK/No cumple|
| 07             | Estructura de proyecto                        | -   | División del proyecto en paquetes del MVC | OK/No cumple|
| 08             | Comprobación fichero `jar`                        | Proyecto a empaquetar   | Se genera y prueba el fichero `jar` empaquetado | OK/No cumple|
| 09             | Creación de branches                        | Parte 1 y parte 2   | Se crean al menos dos branches en el repositorio github | OK/No cumple|
| 10             | Comprobación del botón “Reiniciar” en el menú Edición | Seleccionar “Reiniciar” en el menú | Se vacían los campos y se restablece el estado inicial de la ventana | OK/No cumple |
| 11             | Comprobación de opción “Borrar todo” | Seleccionar “Borrar todo” en el menú Edición | Se elimina el historial mostrado y/o guardado | OK/No cumple |

 
## Parte 3 

Amplía tu proyecto implementando una **prueba automatizada** de interfaz gráfica (GUI test) utilizando la librería *AssertJ Swing*.

El objetivo es comprobar de forma programática que el generador de números aleatorios funciona correctamente cuando el usuario introduce valores en los campos JSpinner y pulsa el botón “Generar”.

1. Asegúrate de incluir las dependencias de *AssertJ Swing* y *JUnit 4* en tu proyecto editando el fichero `pom.xml`.

2. Asegúrate de que los elementos que vayas a tester tengan identificadores (names) asignados a los componentes que vayas a testear.

```java
spinnerMin.setName("spinnerMin");
spinnerMax.setName("spinnerMax");
botonGenerar.setName("botonGenerar");
campoResultado.setName("campoResultado");
```

3. Debes crear en el paquete de VistaControaldor una nueva **clase de prueba** en *Test Packages>new Java Class* que se llame como la clase principal del *JFrame()* acabada en Test.

4. Código de prueba propuesto:

```java
import static org.assertj.core.api.Assertions.assertThat;

import org.assertj.swing.annotation.GUITest;
import org.assertj.swing.edt.FailOnThreadViolationRepaintManager;
import org.assertj.swing.fixture.FrameFixture;
import org.junit.jupiter.api.*;

public class GeneradorNumerosTest {

    private FrameFixture ventana;

   @Before
    public void setUp() {
        // Comprobar que las acciones Swing se hacen en el hilo correcto
        FailOnThreadViolationRepaintManager.install();

        // Inicializar la ventana de prueba en el EDT
        GeneraNumeros frame = GuiActionRunner.execute(() -> new GeneraNumeros()); // <-- Creación segura de la instancia
        
        // Inicializar el FrameFixture
        ventana = new FrameFixture(frame); 
        
        // Mostrar la ventana en el EDT
        ventana.show(); 
    }

    @After
    void tearDown() {
        // Cierra la ventana después de cada prueba
        ventana.cleanUp();
    }

    @Test
    public void deberiaGenerarNumeroAleatorioEntreValoresSpinner() {
        // Introduce los valores en los spinners
        ventana.spinner("spinnerMin").enterText("5");
        ventana.spinner("spinnerMax").enterText("10");

        // Pulsa el botón "Generar"
        ventana.button("botonGenerar").click();

        // Obtiene el resultado mostrado en el JTextField
        String textoResultado = ventana.textBox("campoResultado").text();

        // Convierte el resultado a número y comprueba el rango
        int valor = Integer.parseInt(textoResultado);
        assertThat(valor)
            .as("El número generado debe estar entre 5 y 10")
            .isBetween(5, 10);
    }
}
```

5. Para ejecutar la prueba haz clic sobre la clase y en el menú contextual en *Test File*

6. Agrega dicho caso automatizado a la tabla de pruebas anterior.



