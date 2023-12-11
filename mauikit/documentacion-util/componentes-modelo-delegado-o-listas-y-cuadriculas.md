---
description: >-
  Los componentes modelo-delegado permiten mostrar listas de información, como
  listas de canciones, listas de artistas, listas de archivos, listas de usuario
  o cualquier listado de información.
---

# Componentes modelo-delegado o listas y cuadrículas

* Modelo: son los datos entrantes como nombre de usuario, edad. Es el componente QML ListModel.&#x20;
* Delegado: cómo desea mostrar la información, en una lista, una rejilla o cuadrícula, un rectángulo o cualquier otro componente. Es el componente QML elegido para mostrar los datos.

Se muestran 2 ejemplos:

1. Rellenando el modelo de datos directamente con información definida en el proprio fichero QML.
2. Rellenando el modelo de datos con información procedente de código o funcionalidad C++.

## Ejemplo 1. Rellenando el modelo con datos definidos en el propio fichero QML. Mostrar un menú para Side Bar.

Añada el siguiente código a **main.qml**:

```
import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui

Maui.ApplicationWindow
{
    id: root

    Maui.SideBarView
    {
        anchors.fill: parent

        sideBarContent: Maui.Page
        {
            Maui.Theme.colorSet: Maui.Theme.Window
            anchors.fill: parent

            headBar.visible: false

            ListModel {
            id: mainMenuModel
                ListElement { name: "General behavior" ; description: "Configure other options" ; icon: "love" }
                ListElement { name: "Mouse" ; description: "Adjust mouse behavior" ; icon: "input-mouse" }
                ListElement { name: "Virtual desktops" ; description: "Desktops settings" ; icon: "virtual-desktops" }
            }

            Maui.ListBrowser {
                id: menuSideBar

                anchors.fill: parent
                anchors.margins: 5

                horizontalScrollBarPolicy: ScrollBar.AlwaysOff
                verticalScrollBarPolicy: ScrollBar.AlwaysOff

                currentIndex: 0

                spacing: 5

                model: mainMenuModel

                delegate: Maui.ListBrowserDelegate {
                    width: ListView.view.width
                    height: 60
                    label1.text: name
                    label2.text: description

                    iconSource: icon

                    onClicked: {
                        switch (index) {
                            case 0: {
                                menuSideBar.currentIndex = index
                                //stackView.push("qrc:/Page1.qml")
                                return
                            }
                            case 1: {
                                menuSideBar.currentIndex = index
                                //stackView.push("qrc:/Page2.qml")
                                return
                            }
                            case 2: {
                                menuSideBar.currentIndex = index
                                //stackView.push("qrc:/Page3.qml")
                                return
                            }
                        }
                    }
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
            }
        }
    }
}
```

<figure><img src="../../.gitbook/assets/Modelo-Delegado-Ejemplo-1.png" alt=""><figcaption></figcaption></figure>

currentIndex le permite establecer como seleccionado el correspondiente elemento al pulsar el mismo, mostrándolo con el color de selección, en este caso azul.

Si no desea seleccionar ningún elemento:

```
currentIndex: -1
```

También puede mostrar múltiples páginas de menú usando un StackView:

```
sideBarContent: Maui.Page
{
    Maui.Theme.colorSet: Maui.Theme.Window
    anchors.fill: parent

    headBar.visible: false

    Component.onCompleted: {
        stackMenu.push("qrc:/Menu1.qml")
    }

    StackView {
        id: stackMenu
    }
}
```

Un código usando StackView se muestra en:

{% content-ref url="animaciones.md" %}
[animaciones.md](animaciones.md)
{% endcontent-ref %}

## Ejemplo 2. Rellenando el modelo con datos procedentes de código o funcionalidad C++. Mostrar una lista de usuarios.

1\. Siga los pasos de 1 a 5 indicados en:

{% content-ref url="conectar-funcionalidad-c++-con-la-interfaz-qml.md" %}
[conectar-funcionalidad-c++-con-la-interfaz-qml.md](conectar-funcionalidad-c++-con-la-interfaz-qml.md)
{% endcontent-ref %}

sustituyendo los pasos 1 y 2 por los indicados en el ejemplo final con **QVariantList**.

2\. Añade el siguiente código a **main.qml**

```
import QtQuick 2.15
import QtQuick.Controls 2.15
import org.mauikit.controls 1.3 as Maui
import org.kde.myapp 1.0

Maui.ApplicationWindow
{
    id: root

    Maui.Page
    {
        anchors.fill: parent
        showCSDControls: true

        ListModel {
            id: usersModel
        }

        Component.onCompleted: {
            getUsers()
        }

        function getUsers() {
            var users = Backend.users
            for (var i = 0; i < users.length; i++) {
                usersModel.append({"name": users[i].name,"subname": users[i].subname,"active": users[i].active,"age": users[i].age})
            }
        }

        Maui.ListBrowser {
            id: listUsers

            anchors.fill: parent
            anchors.margins: 5

            horizontalScrollBarPolicy: ScrollBar.AlwaysOff
            verticalScrollBarPolicy: ScrollBar.AlwaysOff

            currentIndex: -1

            spacing: 5

            model: usersModel

            delegate: Maui.ListBrowserDelegate {
                width: ListView.view.width
                height: 60
                label1.text: name + " " + subname
                label2.text: age
            }
        }
    }
}
```

<figure><img src="../../.gitbook/assets/Modelo-Delegado-Ejemplo-2.png" alt=""><figcaption></figcaption></figure>

## Componentes modelo-delegado.

Maui.ListBrowser

{% content-ref url="../controles/listbrowser.md" %}
[listbrowser.md](../controles/listbrowser.md)
{% endcontent-ref %}

Maui.GridBrowser

{% content-ref url="../controles/gridbrowser.md" %}
[gridbrowser.md](../controles/gridbrowser.md)
{% endcontent-ref %}

ListView

{% embed url="https://doc.qt.io/qt-5/qml-qtquick-listview.html" %}

GridView

{% embed url="https://doc.qt.io/qt-5/qml-qtquick-gridview.html" %}

Repeater

{% embed url="https://doc.qt.io/qt-5/qml-qtquick-repeater.html" %}
