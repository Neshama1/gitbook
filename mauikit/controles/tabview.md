---
description: Muestra una vista de pestañas.
---

# TabView

```
import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.ApplicationWindow
{
    id: root

    Maui.TabView
    {
        anchors.fill: parent

        tabBar.rightContent : Switch
        {
        }

        Rectangle
        {
            Maui.TabViewInfo.tabTitle: "Tab 1"
            color: Maui.Theme.backgroundColor
            Label {
                anchors.centerIn: parent
                text: "Tab 1"
            }
        }

        Rectangle
        {
            Maui.TabViewInfo.tabTitle: "Tab 2"
            Maui.TabViewInfo.tabIcon: "love"
            color: Maui.Theme.backgroundColor
            Label {
                anchors.centerIn: parent
                text: "Tab 2"
            }
        }
    }
}
```

<figure><img src="../../.gitbook/assets/Controls-TabView-1.jpg" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Controls-TabView-2.jpg" alt=""><figcaption></figcaption></figure>
