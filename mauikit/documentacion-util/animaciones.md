---
description: Animar una propiedad (x, opacity) es un procedimiento sencillo.
---

# Animaciones

**Efectuar una animación iniciándola explícitamente con la función start().**

El componente stackView permite cargar diversas páginas qml en el mismo espacio o componente padre:

```
stackView.push("qrc:/Home.qml")
stackView.push("qrc:/Users.qml")
```

Añade main.qml, Home.qml y qml.qrc. El código para efectuar la animación se encuentra en Home.qml.

```
// main.qml

import QtQuick 2.15
import QtQuick.Controls 2.15
import QtQuick.Window 2.15
import org.mauikit.controls 1.3 as Maui

Maui.ApplicationWindow
{
    id: root
    title: qsTr("")

    width: Screen.desktopAvailableWidth - Screen.desktopAvailableWidth * 45 / 100
    height: Screen.desktopAvailableHeight - Screen.desktopAvailableHeight * 20 / 100

    Component.onCompleted: {
        stackView.push("qrc:/Home.qml")
    }

    Maui.SideBarView
    {
        id: sideBarView
        anchors.fill: parent

        sideBarContent:  Maui.Page
        {
            id: sideBarPage

            anchors.fill: parent
            Maui.Theme.colorSet: Maui.Theme.Window

            headBar.leftContent: ToolButton {
                icon.name: "start-over"
                onClicked: {
                    stackView.push("qrc:/Home.qml")
                }
            }
        }

        Maui.Page
        {
            anchors.fill: parent

            showCSDControls: true
            headBar.background: null

            StackView {
                id: stackView
                anchors.fill: parent
                clip: true
            }
        }
    }
}
```

```
// Home.qml

import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.Page
{
    id: page

    headBar.visible: false

    Component.onCompleted: {
        opacityAnimation.start()
        xAnimation.start()
    }

    PropertyAnimation {
        id: opacityAnimation
        target: page
        properties: "opacity"
        from: 0
        to: 1.0
        duration: 250

        // Puedes establecer una curva de animación y modificar la intensidad de actuación:
        // easing.type: Easing.InBack
        // easing.overshoot: 10
    }

    PropertyAnimation {
        id: xAnimation
        target: page
        properties: "x"
        from: -20
        to: 0
        duration: 500

        // easing.type: Easing.InBack
        // easing.overshoot: 10
    }


    Maui.SectionGroup
    {
        anchors.left: parent.left
        anchors.right: parent.right
        anchors.top: parent.top
        anchors.margins: 20
        height: 50 * 3

        title: i18n("General")
        description: i18n("Configure the behaviour")

        Maui.SectionItem
        {
            label1.text:  i18n("Desktop search")
            label2.text: i18n("Enable file indexing")
            Switch {
            }
        }

        Maui.SectionItem
        {
            label1.text:  i18n("Global scale")
            label2.text: i18n("Display configuration")
            SpinBox {
                id: spinBox
                from: 0
                to: 100
                value: 50
            }
        }
    }
}
```

```
// qml.qrc

<RCC>
    <qresource prefix="/">
        <file>main.qml</file>
        <file>Home.qml</file>
    </qresource>
</RCC>
```

<figure><img src="../../.gitbook/assets/Doc-Util-Animations.jpg" alt=""><figcaption></figcaption></figure>

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FED1v8xhNFPWKlgOCuryr%2Fuploads%2FSXzvkb46qwM12b5VSmwp%2FDoc-Util-Animations.mp4?alt=media&token=c733f152-d9da-4d6a-840b-5fc6202e4057" %}

**Efectuar una animación un tiempo después de iniciar la aplicación.**

Sustituye Home.qml

```
// Home.qml

import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.Page
{
    id: page

    headBar.visible: false

    opacity: 0

    Component.onCompleted: {
        animationTimer.start()
    }

    Timer {
        id: animationTimer
        interval: 1500; running: false; repeat: false
        onTriggered: {
            opacityAnimation.start()
        }
    }

    PropertyAnimation {
        id: opacityAnimation
        target: page
        properties: "opacity"
        from: 0
        to: 1.0
        duration: 500

        // Puedes establecer una curva de animación y modificar la intensidad de actuación:
        // easing.type: Easing.InBack
        // easing.overshoot: 10
    }

    Maui.SectionGroup
    {
        anchors.left: parent.left
        anchors.right: parent.right
        anchors.top: parent.top
        anchors.margins: 20
        height: 50 * 3

        title: i18n("General")
        description: i18n("Configure the behaviour")

        Maui.SectionItem
        {
            label1.text:  i18n("Desktop search")
            label2.text: i18n("Enable file indexing")
            Switch {
            }
        }

        Maui.SectionItem
        {
            label1.text:  i18n("Global scale")
            label2.text: i18n("Display configuration")
            SpinBox {
                id: spinBox
                from: 0
                to: 100
                value: 50
            }
        }
    }
}
```

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FED1v8xhNFPWKlgOCuryr%2Fuploads%2FN55gmPFXiYDzf8YkLbdP%2FDoc-Util-Animation-Timer.mp4?alt=media&token=0bb3ea0c-d4b6-46a8-9edf-ad437b20336d" %}

**Efectuar una animación cuando la propiedad cambia.**

Sustituye Home.qml

```
// Home.qml

import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.Page
{
    id: page

    headBar.visible: false

    scale: 0.93
    opacity: 0

    Component.onCompleted: {
        scale = 1.0
        opacity = 1.0
    }

    Behavior on scale {
        NumberAnimation {
            duration: 3000
            easing.type: Easing.OutExpo
        }
    }

    Behavior on opacity {
        NumberAnimation { duration: 3000 }
    }

    Maui.SectionGroup
    {
        anchors.left: parent.left
        anchors.right: parent.right
        anchors.top: parent.top
        anchors.margins: 20
        height: 50 * 3

        title: i18n("General")
        description: i18n("Configure the behaviour")

        Maui.SectionItem
        {
            label1.text:  i18n("Desktop search")
            label2.text: i18n("Enable file indexing")
            Switch {
            }
        }

        Maui.SectionItem
        {
            label1.text:  i18n("Global scale")
            label2.text: i18n("Display configuration")
            SpinBox {
                id: spinBox
                from: 0
                to: 100
                value: 50

                property int newValue
                property real newVar: 2.1234

                onValueModified: {
                    var myVar = value
                    console.info(newVar)
                }
            }
        }
    }
}
```

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FED1v8xhNFPWKlgOCuryr%2Fuploads%2FzIMkQfd61MKIQEHhnJk2%2FDoc-Util-Animation-Behavior.mp4?alt=media&token=6a432c9f-df76-41fa-9634-4ffec77b60e0" %}

## Curvas de animación

```
   PropertyAnimation {
        id: opacityAnimation
        target: page
        properties: "opacity"
        from: 0
        to: 1.0
        duration: 500

        // Puedes establecer una curva de animación y modificar la intensidad de actuación:
        // easing.type: Easing.InBack
        // easing.overshoot: 10
    }
```

| Easing.Linear       | Easing curve for a linear (t) function: velocity is constant.                                                                                                                                                                                      |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Easing.InQuad       | Easing curve for a quadratic (t^2) function: accelerating from zero velocity.                                                                                                                                                                      |
| Easing.OutQuad      | Easing curve for a quadratic (t^2) function: decelerating to zero velocity.                                                                                                                                                                        |
| Easing.InOutQuad    | Easing curve for a quadratic (t^2) function: acceleration until halfway, then deceleration.                                                                                                                                                        |
| Easing.OutInQuad    | Easing curve for a quadratic (t^2) function: deceleration until halfway, then acceleration.                                                                                                                                                        |
| Easing.InCubic      | Easing curve for a cubic (t^3) function: accelerating from zero velocity.                                                                                                                                                                          |
| Easing.OutCubic     | Easing curve for a cubic (t^3) function: decelerating to zero velocity.                                                                                                                                                                            |
| Easing.InOutCubic   | Easing curve for a cubic (t^3) function: acceleration until halfway, then deceleration.                                                                                                                                                            |
| Easing.OutInCubic   | Easing curve for a cubic (t^3) function: deceleration until halfway, then acceleration.                                                                                                                                                            |
| Easing.InQuart      | Easing curve for a quartic (t^4) function: accelerating from zero velocity.                                                                                                                                                                        |
| Easing.OutQuart     | Easing curve for a quartic (t^4) function: decelerating to zero velocity.                                                                                                                                                                          |
| Easing.InOutQuart   | Easing curve for a quartic (t^4) function: acceleration until halfway, then deceleration.                                                                                                                                                          |
| Easing.OutInQuart   | Easing curve for a quartic (t^4) function: deceleration until halfway, then acceleration.                                                                                                                                                          |
| Easing.InQuint      | Easing curve for a quintic (t^5) function: accelerating from zero velocity.                                                                                                                                                                        |
| Easing.OutQuint     | Easing curve for a quintic (t^5) function: decelerating to zero velocity.                                                                                                                                                                          |
| Easing.InOutQuint   | Easing curve for a quintic (t^5) function: acceleration until halfway, then deceleration.                                                                                                                                                          |
| Easing.OutInQuint   | Easing curve for a quintic (t^5) function: deceleration until halfway, then acceleration.                                                                                                                                                          |
| Easing.InSine       | Easing curve for a sinusoidal (sin(t)) function: accelerating from zero velocity.                                                                                                                                                                  |
| Easing.OutSine      | Easing curve for a sinusoidal (sin(t)) function: decelerating to zero velocity.                                                                                                                                                                    |
| Easing.InOutSine    | Easing curve for a sinusoidal (sin(t)) function: acceleration until halfway, then deceleration.                                                                                                                                                    |
| Easing.OutInSine    | Easing curve for a sinusoidal (sin(t)) function: deceleration until halfway, then acceleration.                                                                                                                                                    |
| Easing.InExpo       | Easing curve for an exponential (2^t) function: accelerating from zero velocity.                                                                                                                                                                   |
| Easing.OutExpo      | Easing curve for an exponential (2^t) function: decelerating to zero velocity.                                                                                                                                                                     |
| Easing.InOutExpo    | Easing curve for an exponential (2^t) function: acceleration until halfway, then deceleration.                                                                                                                                                     |
| Easing.OutInExpo    | Easing curve for an exponential (2^t) function: deceleration until halfway, then acceleration.                                                                                                                                                     |
| Easing.InCirc       | Easing curve for a circular (sqrt(1-t^2)) function: accelerating from zero velocity.                                                                                                                                                               |
| Easing.OutCirc      | Easing curve for a circular (sqrt(1-t^2)) function: decelerating to zero velocity.                                                                                                                                                                 |
| Easing.InOutCirc    | Easing curve for a circular (sqrt(1-t^2)) function: acceleration until halfway, then deceleration.                                                                                                                                                 |
| Easing.OutInCirc    | Easing curve for a circular (sqrt(1-t^2)) function: deceleration until halfway, then acceleration.                                                                                                                                                 |
| Easing.InElastic    | <p>Easing curve for an elastic (exponentially decaying sine wave) function: accelerating from zero velocity.<br>The peak amplitude can be set with the <em>amplitude</em> parameter, and the period of decay by the <em>period</em> parameter.</p> |
| Easing.OutElastic   | <p>Easing curve for an elastic (exponentially decaying sine wave) function: decelerating to zero velocity.<br>The peak amplitude can be set with the <em>amplitude</em> parameter, and the period of decay by the <em>period</em> parameter.</p>   |
| Easing.InOutElastic | Easing curve for an elastic (exponentially decaying sine wave) function: acceleration until halfway, then deceleration.                                                                                                                            |
| Easing.OutInElastic | Easing curve for an elastic (exponentially decaying sine wave) function: deceleration until halfway, then acceleration.                                                                                                                            |
| Easing.InBack       | Easing curve for a back (overshooting cubic function: (s+1)\*t^3 - s\*t^2) easing in: accelerating from zero velocity.                                                                                                                             |
| Easing.OutBack      | Easing curve for a back (overshooting cubic function: (s+1)\*t^3 - s\*t^2) easing out: decelerating to zero velocity.                                                                                                                              |
| Easing.InOutBack    | Easing curve for a back (overshooting cubic function: (s+1)\*t^3 - s\*t^2) easing in/out: acceleration until halfway, then deceleration.                                                                                                           |
| Easing.OutInBack    | Easing curve for a back (overshooting cubic easing: (s+1)\*t^3 - s\*t^2) easing out/in: deceleration until halfway, then acceleration.                                                                                                             |
| Easing.InBounce     | Easing curve for a bounce (exponentially decaying parabolic bounce) function: accelerating from zero velocity.                                                                                                                                     |
| Easing.OutBounce    | Easing curve for a bounce (exponentially decaying parabolic bounce) function: decelerating to zero velocity.                                                                                                                                       |
| Easing.InOutBounce  | Easing curve for a bounce (exponentially decaying parabolic bounce) function easing in/out: acceleration until halfway, then deceleration.                                                                                                         |
| Easing.OutInBounce  | Easing curve for a bounce (exponentially decaying parabolic bounce) function easing out/in: deceleration until halfway, then acceleration.                                                                                                         |
| Easing.Bezier       | Custom easing curve defined by the easing.bezierCurve property.                                                                                                                                                                                    |

\
**Tipos de actuación sobre cada curva de animación.**

Hay cuatro tipos de actuación sobre la animación, que son aplicables a las correspondientes curvas de animación:

* easing.amplitude: Easing.InBounce, Easing.OutBounce, Easing.InOutBounce, Easing.OutInBounce, Easing.InElastic, Easing.OutElastic, Easing.InOutElastic o Easing.OutInElastic.
* easing.overshoot: Easing.InBack, Easing.OutBack, Easing.InOutBack o Easing.OutInBack.
* easing.period: Easing.InElastic, Easing.OutElastic, Easing.InOutElastic o Easing.OutInElastic.
* easing.bezierCurve: Easing.Bezier. Esta propiedad es un list\<real> conteniendo grupos de tres puntos que definen una curva de 0,0 a 1,1 - control1, control2, end point: \[cx1, cy1, cx2, cy2, endx, endy, ...]. El último punto debe ser 1,1.

**Ejemplos de figuras.**

<figure><img src="../../.gitbook/assets/Figuras-animacion.png" alt=""><figcaption></figcaption></figure>

## Elementos para efectuar animación.

Estos son los cuatro elementos de animación más destacados:

* PropertyAnimation: Efectúa animación en propiedades de controles.
* NumberAnimation: Efectúa animación en valores de tipo qreal.
* ColorAnimation: Efectúa animación en valores de color.
* RotationAnimation: Efectúa animación en valores de rotación.



Otras animaciones más especializadas para diferentes casos de uso:

* PauseAnimation: Permite pausar una animación.
* SequentialAnimation: Permite efectuar animaciones secuencialmente, es decir, una detrás de otra.
* ParallelAnimation: Permite efectuar animaciones en paralelo.
* AnchorAnimation: Permite efectuar animaciones en cambios de anclaje de un control.
* ParentAnimation: Permite efectuar animaciones en cambios de padre de un control, es decir, cuando un control es cambiado de padre.
* SmoothedAnimation: Anima cambios en propiedades vinculadas a un objetivo de manera suave. Una animación efectúa un cambio de un valor origen a un valor destino. Si el valor destino cambia, las curvas de aceleración utilizadas para animar entre los valores de destino antiguo y nuevo se unen suavemente para crear un movimiento suave hacia el nuevo valor de destino. Por tanto permite efectuar animaciones que siguen los cambios de una propiedad, efectuando un cambio en la animación de manera suave.
* SpringAnimation: Permite efectuar animaciones que siguen los cambios de una propiedad imitando como animación el comportamiento oscilatorio de un muelle.
* PathAnimation: Convierte un path en otro path efectuando una animación. Un path es una forma personalizada que puede estar compuesta de múltiples líneas, curvas, arcos, ángulos, etc.
* Vector3dAnimation: Anima cambios en proyecciones tridimensionales.\


Algunas veces es necesario cambiar una propiedad o ejecutar un script durante una animación. Para ello Qt ofrece dos elementos que permiten realizar dicha acción:

* PropertyAction: Especifica cambios de propiedad durante una animación. El cambio de propiedad no es animado.
* ScriptAction: Determina o define la ejecución de scripts durante una animación.



La animación puede ser iniciada de varias formas:

* Animación estándar: es iniciada explícitamente mediante la función start() o estableciendo running a true.
* “Animation on propiedad”: es iniciada después de que el elemento es completamente cargado.
* “Behavior on propiedad”: es iniciada automáticamente cuando la propiedad cambia de valor.
