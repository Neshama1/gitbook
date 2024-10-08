---
description: Muestra elementos es una lista.
---

# ListBrowser

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

        Maui.ListBrowser {
            anchors.fill: parent
            anchors.margins: 20

            horizontalScrollBarPolicy: ScrollBar.AlwaysOff
            verticalScrollBarPolicy: ScrollBar.AlwaysOff

            spacing: 10

            model: 10

            delegate: Rectangle {
                color: "transparent"
                width: ListView.view.width
                height: 80
                Rectangle {
                    anchors.fill: parent
                    anchors.margins: 0
                    radius: 4
                    color: Maui.Theme.alternateBackgroundColor
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

<figure><img src="../../.gitbook/assets/Controls-ListBrowser.jpg" alt=""><figcaption></figcaption></figure>

## ListBrowserDelegate

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

        Maui.ListBrowser {
            anchors.fill: parent
            anchors.margins: 20

            horizontalScrollBarPolicy: ScrollBar.AlwaysOff
            verticalScrollBarPolicy: ScrollBar.AlwaysOff

            spacing: 10

            model: 10

            delegate: Rectangle {
                color: "transparent"
                width: ListView.view.width
                height: 80
                Maui.ListBrowserDelegate
                {
                    anchors.fill: parent
                    anchors.margins: 0
                    label1.text: "An example delegate."
                    label2.text: "Using the MauiKit ListBrowser."

                    iconSource: "folder"
                }
            }
        }
    }
}
```



<figure><img src="../../.gitbook/assets/Controls-ListBrowser-ListBrowserDelegate.jpg" alt=""><figcaption></figcaption></figure>

## Propiedades

{% embed url="https://api.kde.org/mauikit/mauikit/html/classListBrowser.html" %}

{% embed url="https://api.kde.org/mauikit/mauikit/html/classListBrowserDelegate.html" %}
