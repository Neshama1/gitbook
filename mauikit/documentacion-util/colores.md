---
description: Haz que tu aplicación siga el esquema de color del sistema.
---

# Colores

## Set de colores

KDE ha establecido sets de esquemas de colores para las diferentes partes de una apicación:&#x20;

* **Maui.Theme.Window**: set de color por defecto para ventanas y áreas de cromo.
* **Maui.Theme.View**: set de color para las vistas de elementos, normalmente el más claro (en temas claros).
* **Maui.Theme.Button**: set de color usado por botones.
* **Maui.Theme.Selection**: set de color usado por áreas seleccionadas.
* **Maui.Theme.Tooltip**: set de color usado por los globos o descripciones emergentes.
* **Maui.Theme.Complementary**: set de color para ser usado como complemento con Window. Normalmente es oscuro incluso en temas claros. Puede ser usado como énfasis en pequeñas áreas de la aplicación.

```
Maui.Theme.colorSet: Maui.Theme.View
```

Al definir un set es heredado por todos los componentes hijo, a menos que se especifique lo contrario mediante:

```
Maui.Theme.inherit: false
```

```
import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.ApplicationWindow
{
    id: root

    Maui.SideBarView
    {
        anchors.fill: parent

        sideBarContent: Maui.Page
        {
            // COLOR SET
            Maui.Theme.colorSet: Maui.Theme.View

            anchors.fill: parent

            headBar.leftContent: Maui.ToolButtonMenu
            {
                icon.name: "application-menu"
                MenuItem
                {
                    text: "About"
                    icon.name: "info-dialog"
                    onTriggered: root.about()
                }
            }

            headBar.rightContent: ToolButton
            {
                icon.name: "love"
            }
        }

        Maui.Page
        {
            anchors.fill: parent
            showCSDControls: true
        }
    }
}
```

<figure><img src="../../.gitbook/assets/Util-Colores.jpg" alt=""><figcaption></figcaption></figure>

Si establecemos:

```
Maui.Theme.colorSet: Maui.Theme.Window
```

<figure><img src="../../.gitbook/assets/Util-Colores-1.jpg" alt=""><figcaption></figcaption></figure>

## Cambiar el color de una página.

Establezca un "background" para la página y para la headBar.

```
import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.ApplicationWindow
{
    id: root

    Maui.SideBarView
    {
        anchors.fill: parent

        sideBarContent: Maui.Page
        {
            // COLOR SET
            Maui.Theme.colorSet: Maui.Theme.Window

            anchors.fill: parent

            headBar.leftContent: Maui.ToolButtonMenu
            {
                icon.name: "application-menu"
                MenuItem
                {
                    text: "About"
                    icon.name: "info-dialog"
                    onTriggered: root.about()
                }
            }

            headBar.rightContent: ToolButton
            {
                icon.name: "love"
            }

            headBar.background: Rectangle {
                anchors.fill: parent
                color: Qt.lighter(Maui.Theme.backgroundColor,1.035)
            }

            background: Rectangle {
                anchors.fill: parent
                color: Qt.lighter(Maui.Theme.backgroundColor,1.035)
            }
        }

        Maui.Page
        {
            anchors.fill: parent
            showCSDControls: true
        }
    }
}
```

<figure><img src="../../.gitbook/assets/Util-Colores-3.jpg" alt=""><figcaption></figcaption></figure>

## Colores del sistema

Los colores de sistema dependen del set de color establecido y del esquema seleccionado por el usuario de KDE.

* Maui.Theme.textColor
* Maui.Theme.disabledTextColor
* Maui.Theme.highlightColor
* Maui.Theme.highlightedTextColor
* Maui.Theme.backgroundColor
* Maui.Theme.alternateBackgroundColor
* Maui.Theme.focusColor
* Maui.Theme.hoverColor
* Maui.Theme.activeTextColor
* Maui.Theme.activeBackgroundColor
* Maui.Theme.linkColor
* Maui.Theme.linkBackgroundColor
* Maui.Theme.visitedLinkColor
* Maui.Theme.visitedLinkBackgroundColor
* Maui.Theme.negativeTextColor
* Maui.Theme.negativeBackgroundColor
* Maui.Theme.neutralTextColor
* Maui.Theme.neutralBackgroundColor
* Maui.Theme.positiveTextColor
* Maui.Theme.positiveBackgroundColor
* Maui.Theme.buttonTextColor
* Maui.Theme.buttonBackgroundColor
* Maui.Theme.buttonAlternateBackgroundColor
* Maui.Theme.buttonHoverColor
* Maui.Theme.buttonFocusColor
* Maui.Theme.viewTextColor
* Maui.Theme.viewBackgroundColor
* Maui.Theme.viewAlternateBackgroundColor
* Maui.Theme.viewHoverColor
* Maui.Theme.viewFocusColor
* Maui.Theme.selectionTextColor
* Maui.Theme.selectionBackgroundColor
* Maui.Theme.selectionAlternateBackgroundColor
* Maui.Theme.selectionHoverColor
* Maui.Theme.selectionFocusColor
* Maui.Theme.tooltipTextColor
* Maui.Theme.tooltipBackgroundColor
* Maui.Theme.tooltipAlternateBackgroundColor
* Maui.Theme.tooltipHoverColor

```
color: "#0FC092"
color: "#550FC092"    // Color con transparencia alpha 55 hexadecimal
color: "transparent"
color: "mediumspringgreen"
color: Maui.Theme.focusColor
```

```
import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.ApplicationWindow
{
    id: root

    Maui.Page {
        anchors.fill: parent
        showCSDControls: true

        Rectangle {
            anchors.centerIn: parent
            width: 200
            height: 200
            color: Maui.Theme.focusColor
            radius: 4
        }
    }
}
```

<figure><img src="../../.gitbook/assets/Util-Colores-2.jpg" alt=""><figcaption></figcaption></figure>

## Aclarar u oscurecer un color.

```
color: Qt.lighter(Maui.Theme.backgroundColor, 1.2)
color: Qt.darker(Maui.Theme.backgroundColor, 2)
color: Qt.lighter("#0FC092", 1.5)
color: Qt.lighter("#550FC092", 1.5)
```

## Color en función de tema claro u oscuro

```
color: Maui.ColorUtils.brightnessForColor(Maui.Theme.backgroundColor) == Maui.ColorUtils.Light ? Qt.lighter(Maui.Theme.alternateBackgroundColor,1.01) : Qt.lighter(Maui.Theme.alternateBackgroundColor,1.08)
```

## Colores predefinidos

Consulte la tabla de colores predefinidos.

{% embed url="https://doc.qt.io/qt-5/qml-color.html" %}

## Opacidad

Los componentes QML incluyen la propiedad "opacity" que le permite especificar un grado de transparencia entre opaco (1) y transparente(0). Permite integrar un color o una imagen con el fondo tanto en temas claros como oscuros. Otras aplicaciones incluyen establecer fondo translúcido para tu aplicación o efectuar animación en la opacidad del control.

```
import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.ApplicationWindow
{
    id: root

    Maui.Page {
        anchors.fill: parent

        showCSDControls: true

        Maui.IconItem
        {
            anchors.centerIn: parent
            imageSource: "https://upload.wikimedia.org/wikipedia/commons/8/8d/KDE_logo.svg"
            imageSizeHint: 200
            maskRadius: Maui.Style.radiusV
            fillMode: Image.PreserveAspectCrop
            opacity: 0.04
        }
    }
}

```
