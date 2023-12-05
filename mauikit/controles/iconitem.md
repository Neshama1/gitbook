---
description: Muestra un icono o imagen.
---

# IconItem

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
        }
    }
}

```

```
imageSource: "qrc:/assets/6588168.jpg"
```

<figure><img src="../../.gitbook/assets/Controls-IconItem.jpg" alt=""><figcaption></figcaption></figure>

## Propiedades

{% embed url="https://api.kde.org/mauikit/mauikit/html/classIconItem.html" %}
