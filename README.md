# Práctica 2.4 Generador de números aleatorios

El objetivo de esta práctica es la de diseñar y desarrollar una aplicación gráfica que permita generar **números aleatorios** dentro de un **rango** definido por el usuario, aplicando los principios de separación básica entre la interfaz y la lógica de la aplicación (Modelo y VistaControlador).

Durante la práctica se trabajará con componentes Swing, FlatLaf, colecciones, diálogos, lectura y escritura de ficheros y empaquetado de aplicaciones Maven.

Además, se introducirán dos niveles diferentes de pruebas automatizadas:

- pruebas unitarias para comprobar la lógica de la aplicación;
- pruebas de interfaz gráfica para comprobar la interacción del usuario con la ventana.

## Preparación del proyecto

Crea dentro de la carpeta `SOL` de tu repositorio local un nuevo proyecto Maven de Apache NetBeans llamado:

`practica2-4`

El proyecto deberá utilizar **FlatLaf**, añadiendo la dependencia correspondiente mediante Maven.

Desde el comienzo se organizarán las clases en dos paquetes:

```
Modelo
VistaControlador
```

Utiliza ramas para separar las distintas partes de la práctica:

- `parte-1`
- `parte-2`
- `parte-3`
- `parte-4`


## Parte 1 Generador de números aleatorios

Crea mediante el editor visual de Apache NetBeans una ventana que permita generar un número aleatorio dentro de un rango indicado por el usuario.

La interfaz deberá contener como mínimo:

- un `JSpinner` para indicar el valor mínimo;
- un `JSpinner` para indicar el valor máximo;
- un `JButton` denominado **Generar**;
- un `JTextField` no editable para mostrar el resultado;
- una barra de menú mediante `JMenuBar`.

La aplicación deberá iniciarse utilizando **FlatLaf**.

### Generación de números aleatorios

Crea dentro del paquete `Modelo` una clase llamada `GeneradorNumeros`

> ⚠️ La generación del número aleatorio **no deberá realizarse directamente dentro del evento del botón**.

Ayúdate de la función `Math.random()` entre dos números o de la clase `radom` así como de una **clase auxiliar** para realizar dichos cálculos.

```java
Math.random() * (max - min + 1) + (min)
```

```java
Random rnd = new Random();
rnd.nextDouble() * max + min
```

Antes de realizar la generación deberá verificarse si el rango indicado es correcto, o deberá mostrarse un mensaje mediante `JOptionPane`.

### Menú de la aplicación

Añade los siguientes menús:

```text
Fichero
Edición
```

Dentro del menú **Fichero**:
- La opción **salir** que deberá cerrar la aplicación.

Dentro del menú **edición**:
- La opción **Reiniciar** deberá restablecer los valores de los `JSpinner` y devolver los campos de la aplicación a su estado inicial.

![](media/ba18dcfdd7fd2df3ed8dfe1cefa04f24.png)

## Parte 2 Números primos, historial y ficheros

Amplía ahora la aplicación con nuevas funcionalidades.

### Generación de números primos 

Agrega un *checkbox* que en caso de estar marcado solo permita mostrar números **primos** entre los rangos indicados.

La comprobación de si un número es primo deberá realizarse completamente dentro del paquete `Modelo`.

### Historial de números generados

Agrega en el *menú edición* la siguiente opción: 
- Una opción llamada **historial** que permita ver los últimos números generados.
- Otra opción llamada **borrar todo** para eliminar el listado guardado del historial.

Para ello deberás utilizar en una ventana modal (*JDialog*). Esta ventana conted´ra una lista (*JList*). Puedes editar la disposición de dicha ventana de diálogo desde el editor de Netbeans en la pestaña del *Navigator* en *Other Components*. 

Puedes utilizar una colección como ``ArrayList<Integer>``  para almacenarlos.

El historial deberá pertenecer a la lógica de la aplicación y no únicamente a los componentes gráficos.

Antes de borrar el contenido del historial la operación deberá solicitar confirmación mediante un `JOptionPane`.

### Guardar historial en un fichero

Agrega en el *menú fichero* la opción **guardar historial**.

Para guardar dicho historial del listado se ha de utilizar un *JFileChooser* para permitir al usuario seleccionar la ubicación y el nombre del fichero. 

El historial deberá guardarse en un fichero de texto.

Por ejemplo:

```text
Historial de números generados:
23
17
41
8
```

Se deberá verificar si ya existe un fichero con el mismo nombre antes de sobreescribirlo.  

> No olvides gestionar los errores mediante try-catch dentro del código de la aplicación.

## Pruebas (testing)

### Pruebas unitarias



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

 
### Prueba automatizada de la interfaz

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



