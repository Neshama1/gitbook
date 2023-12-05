---
description: Muestra acciones agrupadas.
---

# ToolActions

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

        Maui.ToolActions
        {
            anchors.centerIn: parent

            Action
            {
                icon.name: "draw-arrow-back"
            }
            Action
            {
                icon.name: "draw-arrow-forward"
            }
        }
    }
}

```

<figure><img src="../../.gitbook/assets/Controls-ToolActions.jpg" alt=""><figcaption></figcaption></figure>

## Propiedades

{% embed url="https://api.kde.org/mauikit/mauikit/html/classToolActions.html" %}
