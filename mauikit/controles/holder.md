---
description: Muestra un mensaje informativo junto con acciones.
---

# Holder

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

        Maui.Holder
        {
            anchors.fill: parent
            title: i18n("Holder")
            body: i18n("Holder body message with quick info")
            emoji: "folder"
            isMask: false

            Action
            {
                text: "Action1"
            }
            Action
            {
                text: "Action2"
            }
        }
    }
}

```

<figure><img src="../../.gitbook/assets/Controls-Holder.jpg" alt=""><figcaption></figcaption></figure>

## Propiedades

{% embed url="https://api.kde.org/mauikit/mauikit/html/classHolder.html" %}
