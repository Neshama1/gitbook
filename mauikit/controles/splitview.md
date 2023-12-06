---
description: Proporciona una vista dividida de aplicación.
---

# SplitView

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

        Maui.SplitView
        {
            anchors.fill: parent

            Maui.SplitViewItem
            {
                Rectangle
                {
                    anchors.fill: parent
                    color: Maui.Theme.alternateBackgroundColor
                }
            }

            Maui.SplitViewItem
            {
                Rectangle
                {
                    anchors.fill: parent
                    color: Maui.Theme.alternateBackgroundColor
                }
            }
        }
    }
}
```

<figure><img src="../../.gitbook/assets/Controls-SplitView (1).jpg" alt=""><figcaption></figcaption></figure>

## Propiedades

{% embed url="https://api.kde.org/mauikit/mauikit/html/classSplitView.html" %}
