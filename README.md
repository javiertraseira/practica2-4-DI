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

## Pruebas (testing) 

| ID Caso Prueba | Descripción Caso de Prueba               | Entrada                          | Salida Esperada                                                                 | Resultado   |
|----------------|-----------------------------------------|----------------------------------|---------------------------------------------------------------------------------|-------------|
| 01             | Verificar campos de texto (JTextField)  | Escribir texto en los campos     | Se duplican en la otra mitad                                                     | OK/No cumple|
| 02             | Verificar Radio Buttons (JRadiobutton)   | Modificar Radio buttons          | Se duplican en la otra mitad                                                     | OK/No cumple|
| 03             | Verificar Check Buttons (JCheckbox)      | Modificar Check Box              | Se duplican en la otra mitad                                                     | OK/No cumple|
| 04             | Verificar Listado (JCombobox)            | Modificar Combobox               | Se duplican en la otra mitad                                                     | OK/No cumple|
| 05             | Verificar Spinner (JSpinner)             | Modificar Spinner                | Se duplican en la otra mitad                                                     | OK/No cumple|
| 06             | Verificar Barra deslizadora              | Deslizar barra                   | Se duplican en la otra mitad                                                     | OK/No cumple|
| 07             | Verificar Toggle Botón (JToggleButton)   | Pulsar botón                     | Se duplican en la otra mitad                                                     | OK/No cumple|
| 08             | Validación campo correo                  | Escribir un correo electrónico usando su formato con @ | Se valida mostrando un borde en color rojo hasta que su formato sea correcto | OK/No cumple|
