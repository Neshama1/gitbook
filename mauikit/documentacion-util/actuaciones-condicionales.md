---
description: Evalúe condiciones en QML.
---

# Actuaciones condicionales

```
Rectangle {
    id: rect
    width: 200
    height: 200
    color: mouse.hovered ? "mediumspringgreen" : "deeppink"
    radius: 4
    HoverHandler {
        id: mouse
    }
}
```

```
property bool selected
text: selected ? "scheme selected" : ""
text: selected == true ? "scheme selected" : ""
text: selected == false ? "" : "scheme selected"
```

```
property real luminance
color: luminance > 0.5 ? "mediumspringgreen" : "deeppink"
color: luminance <= 0.5 ? "deeppink" : "mediumspringgreen"
```

```
property real luminance
color: {
    if (luminance > 0.5) {
        return "mediumspringgreen"
    }
    else {
        return "deeppink"
    }
}
```

```
property bool condition1: true
property bool condition2: true
if (luminance > 0.5 && luminance < 0.8)        // Y: deben cumplirse ambos
if (condition1 == true || condition2 == true)  // O: debe cumplirse 1 u otro 
if (condition1 || condition2)
```

```
property int option: 1
property color mycolor: "#9333b1"

color: {
    switch (option) {
        case 1: {
            return Qt.darker(mycolor, 2.0)
        }
        case 2: {
            return Qt.lighter(mycolor, 2.0)
        }
    }
}
```
