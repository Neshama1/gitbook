---
description: Conceptos aclaratorios.
---

# Aclaración

Las aplicaciones MauiKit y Qt/QML operan de este modo:

1. Funcionalidad: implementada en C++, python, etc. Preferentemente C++.
2. Interfaz: implementada en QML. Puede añadir código y funciones javascript directamente en los ficheros QML.

Tenga en cuenta:

* Aquello que defina en **main.qml** es definido **globalmente**, siendo disponible en cualquier fichero qml.
* Aquello que defina en otro archivo qml es definido localmente.

## Controles QML

Debe entender:

* Puede declarar propiedades en la definición del componente QML, pero no en los eventos de respuesta onClicked, onTriggered, etc: property string myText.
* Dentro de un evento de respuesta onClicked declare variables tipo "var" si es necesario, que pueden tomar cualquier valor.
* Convierta de var a string con myVar.toString().
* En la definición del componente se iguala con ":".
* En los eventos de respuesta onClicked, onTriggered, etc, se iguala con "=".
* Evalúe propiedades o variables en los eventos de respuesta onClicked, etc, mediante: console.info(myPropertie). Será visualizado en el panel Debug de KDevelop.

```
Button {
    id: button
    property string myText: "test 1"
    onClicked: {
        var myVar = "test 2"
        myText = myVar.toString()
        console.info(myText)
    }
}
```

```
property string myText: "my text"
property int myNumber: 50
property bool myValue: false    // false, true
property real myNum1: 2.1547
property double myNum2: 2.1547
```

