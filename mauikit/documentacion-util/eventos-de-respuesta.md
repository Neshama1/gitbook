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
