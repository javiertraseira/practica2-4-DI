# Práctica 2.4 – Elementos interfaz mixta

## Parte 1

Crear una interfaz mixta con los elementos indicados y con ellos duplicados en espejo, en la que los cambios en la primera parte de la interfaz, sea una imagen para la otra mitad de forma inmediata, excepto al primer campo de texto, que deberá mostrar el duplicado con el texto en *orden inverso*.

Para ello habrá que hacer uso de los **eventos** relacionados con cada componente, para duplicarlos en su correspondiente elemento. 

Se hará uso de los siguientes **controles clásicos** de una interfaz:

-   *2 Campos de texto (JTextField)*
-   *3 Radio buttons (JRadiobutton)*
-   *3 Casillas verificación (JCheckbox)*
-   *1 Listado (JCombobox)*
-   *1 Barra deslizadora (JSlider)*
-   *1 JSpinner*
-   *1 JToggleButton*


Añade igualmente una **barra de estado inferior** haciendo uso de un *JPane*, la cual usaremos posteriormente.

![](media/b659313c2f89bf08a4f35281a33b65c3.png)

## Parte 2

Mejora el ejercicio anterior agregando una **validación** en tiempo real del campo de texto del **correo** en el que verifique que esté correctamente formado. 
- Mientras la validación del correo no sea correcta deberá de mostrar el cuadro de texto con un **borde en color rojo**.
- Al validarse correctamente, deberá mostrar un **icono** de un tic de validación en verde a la derecha y un mensaje en la **barra de estado** inferior.
