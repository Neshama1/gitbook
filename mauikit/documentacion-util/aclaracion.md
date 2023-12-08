---
description: Conceptos aclaratorios.
---

# Aclaración

Las aplicaciones MauiKit y Qt/QML operan de este modo:

1. Funcionalidad: implementada en C++, python, etc. Preferentemente C++.
2. Interfaz: implementada en QML. Puede añadir código y funciones javascript directamente en los ficheros QML.

Tenga en cuenta:

* Aquello que defina en **main.qml** es definido **globalmente**, siendo disponible en cualquier fichero qml.
* Aquello que defina en otro archivo qml es definido localmente.

