---
description: >-
  Esta página facilita de forma rápida el evento de respuesta característico de
  cada componente.
---

# Eventos de respuesta

**Evento OnClicked.**

```
Button {
    id: button
    onClicked: {
    }
}
```

Controles:

* Button
* CheckBox
* RoundButton
* ToolButton
* MenuItem
* Maui.GridBrowserDelegate
* Maui.ListBrowserDelegate
* Maui.SwipeBrowserDelegate
* Maui.GalleryRollItem
* Maui.CollageItem
* Maui.Badge
* Maui.FloatingButton
* Maui.Chip
* Maui.CloseButton
* Maui.ToolBar > ToolButton
* Maui.ToolButtonMenu > MenuItem

**Evento onTriggered.**

```
Action
{
    icon.name: "love"
    onClicked: {        
    }
}
```

Controles:

* Action
* Maui.MenuItemActionRow > Action
* Maui.ToolActions > Action
* Maui.Holder > Action

**Evento onAccepted.**

```
Maui.SearchField
{
    placeholderText: "Search for..."
    onAccepted: {
        console.info(text)
    }
}
```

Controles:

* Maui.SearchField
* ComboBox
* TextField

**Eventos particulares.**

ColorsRow

```
Maui.ColorsRow
{
    anchors.centerIn: parent
    colors: ["pink", "mediumspringgreen", "deepskyblue", "royalblue"]
    onColorPicked: {
        console.info(color)
    }
}

```

Slider

```
Slider {
    from: 0
    value: 0
    to: 100
    onMoved: {
        console.info(value)
    }
}
```

Spinbox

```
SpinBox {
    from: 5
    to: 500
    value: 100

    onValueModified: {
        console.info(value)
    }
}
```

Switch

```
Switch {
    checkable: true
    checked: fileIndexing ? true : false
    onToggled: {
        console.info(visualPosition) // 0 ó 1
    }
}
```

## Capturar los eventos del ratón en otros controles.

Es posible usar MouseHandler o HoverHandler para capturar los eventos del ratón en cualquier control. Útil para controles:

* Rectangle
* Maui.ShadowedRectangle
* Maui.Page
* Maui.IconItem
* Maui.ListItemTemplate

**MouseArea**

```
Rectangle {
    anchors.centerIn: parent
    width: 200
    height: 200
    radius: 4
    color: Maui.Theme.alternateBackgroundColor
    MouseArea {
        anchors.fill: parent
        onClicked: {
            console.info("evento de ratón pulsado")
        }
    }
}
```

**HoverHandler**

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
            radius: 4
            color: mouse.hovered ? Maui.Theme.focusColor : Maui.Theme.alternateBackgroundColor
            HoverHandler {
                id: mouse
            }
        }
    }
}

```
