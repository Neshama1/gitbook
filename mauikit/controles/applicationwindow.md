# ApplicationWindow

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
        }
        
        Maui.Page
        {
            anchors.fill: parent
            showCSDControls: true
        }
    }
}

```

showCSDControls: Muestra u oculta los botones de maximizar, minimizar y restaurar. Valores: true, false

headBar.visible Valores: true, false

headBar.farLeftContent

headBar.leftContent

headBar.middleContent

headBar.rightContent

headBar.farRightContent

headBar.background Valores: Item / componente

sideBar.preferredWidth: Establece anchura de la Side Bar. Ej: Maui.Style.units.gridUnit \* 15

#### Establecer anchura y altura default.

```
import QtQuick.Window 2.15

// En Maui.ApplicationWindow
width: Screen.desktopAvailableWidth - Screen.desktopAvailableWidth * 45 / 100
height: Screen.desktopAvailableHeight - Screen.desktopAvailableHeight * 25 / 100
```

#### Uso de Blur y transparencia.

Este ejemplo aplica blur y transparencia en la Side Bar.

```
// En Maui.ApplicationWindow

Loader
{
    active: Maui.Handy.isLinux
    asynchronous: true
    sourceComponent: Maui.WindowBlur
    {
        view: root
        geometry: Qt.rect(root.x, root.y, root.width, root.height)
        enabled: true
    }
}

// En sideBarContent: Maui.Page

headBar.background: null

background: Rectangle {
    anchors.fill: parent
    color: Maui.Theme.backgroundColor
    opacity: 0.50
}
```

```
```
