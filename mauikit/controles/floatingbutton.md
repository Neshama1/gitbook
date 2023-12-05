---
description: Muestra un botón flotante.
---

# FloatingButton

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

        headBar.background: null

        Maui.FloatingButton
        {
            icon.name: "love"
            anchors.bottom: parent.bottom
            anchors.right: parent.right
            anchors.margins: 20
        }
    }
}

```

<figure><img src="../../.gitbook/assets/Controls-FloatingButton.jpg" alt=""><figcaption></figcaption></figure>

## Propiedades

{% embed url="https://api.kde.org/mauikit/mauikit/html/classFloatingButton.html" %}
