---
description: Muestra elementos en una rejilla o cuadrícula.
---

# GridBrowser

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

        Maui.GridBrowser {
            anchors.fill: parent
            anchors.margins: 20
            itemSize: 100
            itemHeight: 100
            adaptContent: true
            horizontalScrollBarPolicy: ScrollBar.AlwaysOff
            verticalScrollBarPolicy: ScrollBar.AlwaysOff

            model: 20

            delegate: Rectangle {
                color: "transparent"
                width: GridView.view.cellWidth
                height: GridView.view.cellHeight
                Rectangle {
                    anchors.fill: parent
                    anchors.margins: 10
                    radius: 4
                    color: "pink"
                }
            }
        }
    }
}


```

```
horizontalScrollBarPolicy: ScrollBar.AsNeeded, ScrollBar.AlwaysOn, ScrollBar.AlwaysOff
verticalScrollBarPolicy: ScrollBar.AsNeeded, ScrollBar.AlwaysOn, ScrollBar.AlwaysOff
```

<figure><img src="../../.gitbook/assets/Controls-GridBrowser (1).jpg" alt=""><figcaption></figcaption></figure>

## Propiedades

{% embed url="https://api.kde.org/mauikit/mauikit/html/classGridBrowser.html" %}
