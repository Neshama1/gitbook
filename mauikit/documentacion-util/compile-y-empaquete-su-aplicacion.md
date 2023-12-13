---
description: >-
  Compile y empaqute su aplicación MauiKit para Nova Flow OS / openSUSE
  Tumbleweed.
---

# Compile y empaquete su aplicación

Tomando como ejemplo la aplicación MauiKit base (mauimusic) creada como se indica en:

{% content-ref url="../../qt-qml-en-imagenes/mauikit/" %}
[mauikit](../../qt-qml-en-imagenes/mauikit/)
{% endcontent-ref %}

#### 1. Registre una cuenta en Open Build Service:

{% embed url="https://openbuildservice.org" %}

{% embed url="https://build.opensuse.org" %}

#### 2. Crear un subproyecto y añadir el repositorio MauiKit:

* En la página se subproyecto verá: Overview, Repositories, Monitor, Requests, etc.
*   Seleccione Repositories > Add from a project:

    * Project: home:hopeandtruth6517:mauikit-apps
    * Repositories: openSUSE\_Tumbleweed
    * Name: mauikit-apps\_Tumbleweed
    * Architectures: i586, x86\_64

    El repositorio mauikit-apps depende a su vez del repositorio de openSUSe Tumbleweed, por lo que el repositorio añadido a su subproyecto tiene acceso a los 2 repositorios.

#### 3. Seleccionar el subproyecto y crear un paquete:

* Name: mauimusic
* Title: Maui Music
* Description: Discover and listen music

#### 3. De un modo sencillo (sin integración git):

* Elimine la carpeta mauimusic/build si ha compilado y ejecutado localmente.
* Haga una copia de la carpeta mauimusic y renómbrela mauimusic-0.1.0.
* Con el gestor de archivos Dolphin, haga click sobre la carpeta mauimusic-0.1.0 y seleccione Compress > Here as "mauimusic-0.1.0.tar.gz"
* Suba el archivo en Open Build Service: Add local files.

#### 4. En la página de paquete mauimusic seleccione:

* Add an empty file or service > Filename: mauimusic.spec

#### 5. Añade a mauimusic.spec:

<pre><code>%define mauikit_version 3.0.1

Name:           mauimusic
Version:        0.1.0
Release:        0
License:        LGPL-3.0
Summary:        Discover and listen music
URL:            https://github.com/user/mauimusic
Source:         %{name}-%{version}.tar.gz

%if 0%{?sle_version} == 150400 &#x26;&#x26; 0%{?is_opensuse} 
ExcludeArch: x86_64
%endif

%if 0%{?sle_version} == 150500 &#x26;&#x26; 0%{?is_opensuse} 
ExcludeArch: x86_64
%endif

BuildRequires:  gcc-c++
BuildRequires:  cmake
BuildRequires:  extra-cmake-modules
BuildRequires:  fdupes
BuildRequires:  AppStream

BuildRequires:  cmake(Qt5QuickCompiler)
BuildRequires:  cmake(Qt5Core)
BuildRequires:  cmake(Qt5Quick)
BuildRequires:  cmake(Qt5Qml)
BuildRequires:  cmake(Qt5Widgets)

BuildRequires:  cmake(KF5I18n)
BuildRequires:  cmake(KF5CoreAddons)

BuildRequires:  cmake(MauiKit) = %{mauikit_version}
BuildRequires:  cmake(MauiKitFileBrowsing) = %{mauikit_version}

Requires:       qt5qmlimport(QtQuick.Controls.2)
Requires:       qt5qmlimport(QtQuick.Layouts.1)

Requires:       mauikit = %{mauikit_version}
Requires:       mauikit-filebrowsing = %{mauikit_version}

%description
Discover and listen music.

<strong>%prep
</strong>%autosetup -p1

%build
%cmake_kf5 -d build
%cmake_build

%install
%kf5_makeinstall -C build
%kf5_post_install
%fdupes %{buildroot}%{_prefix}

%files
%license licenses/*
%doc README.md
%{_bindir}/mauimusic
%{_datadir}/applications/*.desktop
%{_datadir}/metainfo/*.xml
%{_datadir}/icons/hicolor/*/*/*

%changelog
</code></pre>

La aplicación debería compilar exitosamente: **succeeded**

## El fichero spec.

De un modo práctico con cada aplicación sólo tendrá que rellenar:

* Name, Versión, License, Summary, URL.
* BuildRequires y Requires.
* Description.
* Files.

**BuildRequires:**

Son los requerimientos durante la compilación. Son paquetes "**devel**".

* mauimusic/CMakeLists.txt (busque todas las líneas **find\_package**):
* mauimusic/src/CMakeLists.txt (busque todo en **target\_link\_libraries**)

```
find_package(ECM ${REQUIRED_KF5_VERSION} REQUIRED NO_MODULE)

find_package(Qt5 ${QT_MIN_VERSION} REQUIRED COMPONENTS Core Quick Qml Widgets)
find_package(KF5 ${KF5_MIN_VERSION} REQUIRED COMPONENTS I18n CoreAddons)

find_package(Qt5QuickCompiler)
set_package_properties(Qt5QuickCompiler PROPERTIES
    DESCRIPTION "Compile QML at build time"
    TYPE OPTIONAL
    )

find_package(MauiKit3)
find_package(MauiKit3 REQUIRED COMPONENTS FileBrowsing)
```

```
target_link_libraries(${PROJECT_NAME}
    PRIVATE
    MauiKit3
    MauiKit3::FileBrowsing

    Qt5::Core
    Qt5::Quick
    Qt5::Widgets

    KF5::CoreAddons
    KF5::I18n
    )
```

Cada uno de ellos es un requerimiento de compilación y debe ser incluido como BuildRequires.

Abra Gestión de Software de YaST:

* Qt5Core / paquete libQt5Core-devel / dependencias > proporciona: cmake(Qt5Core)
* KF5I18n / paquete ki18n-devel / dependencias > proporciona: cmake(KF5I18n)

Para buscar el paquete que corresponde a cmake(Qt5Core), indíquelo en:

{% embed url="https://pkgs.org/" %}

Si ha encontrado la librería binaria compilada y desea conocer el paquete devel tambien puede buscarlo en:

* libKF5I18n5

{% embed url="https://software.opensuse.org" %}

Seleccione en los resultados: libKF5I18n5 > official release > ki18n.spec:

* Name: ki18n
* %package devel: nombre resultante ki18n-devel
* %package addon: nombre resultante ki18n-addon (ejemplo, no existe)

o bien:

* %define lname libKF5I18n5
* %package -n %{lname}: nombre resultante libKF5I18n5
* %package -n libMusic: nombre resultante libMusic

**Requires:**

Paquetes requeridos durante la instalación.

1. Paquetes binarios de cada librería.
2. Paquetes correspondientes a cada "import".

Dado que vienen instalados por defecto es costumbre no indicarlos, pero es necesario incluirlo si no se encuentra instalado.

Para comprobar los import:

* Instale Bluefish.
* Navegar hasta mauimusic > click derecho o secundario ratón sobre mauimusic > Buscar archivos:
* Escriba: import y click "buscar todos".

```
import QtQuick.Controls 2.15
import QtQuick.Layouts 1.12
```

```
Requires:       qt5qmlimport(QtQuick.Controls.2)
Requires:       qt5qmlimport(QtQuick.Layouts.1)
```

Comprobando en:

{% embed url="https://pkgs.org" %}

* qt5qmlimport(QtQuick.Controls.2) es: libqt5-qtquickcontrols2-5.15.11+kde5-1.1.x86\_64.rpm
* qt5qmlimport(QtQuick.Layouts.1) es: qtdeclarative-imports-provides-qt5-1.0-1.22.x86\_64.rpm

#### Files

Indicados en mauimusic/CMakeLists.txt

```
project(mauimusic VERSION 1.0)
install(FILES src/data/project.appdata.xml DESTINATION ${KDE_INSTALL_METAINFODIR} RENAME ${PROJECT_URI}.appdata.xml)
install(FILES src/data/project.desktop DESTINATION ${XDG_APPS_INSTALL_DIR} RENAME ${PROJECT_URI}.desktop)
install(FILES src/assets/logo.svg DESTINATION ${KDE_INSTALL_ICONDIR}/hicolor/scalable/apps RENAME ${PROJECT_NAME}.svg)
```

Si alguna vez compila una aplicación y no sabe que archivos se instalan, no incluya nada en la sección Files y compile. Si la compilación es correcta, producirá "failed" antes de empaquetar, pero le indicará los archvos y rutas de instalación.

El nombre del ejecutable o binario es el nombre del proyecto:

```
project(mauimusic VERSION 1.0)
```

```
// mauimusic.spec

%files
%license licenses/*
%doc README.md
%{_bindir}/mauimusic
%{_datadir}/applications/*.desktop
%{_datadir}/metainfo/*.xml
%{_datadir}/icons/hicolor/*/*/*
```

```
// mauimusic.spec

%files
%license licenses/*
%doc README.md
/usr/bin/mauimusic
/usr/share/applications/*.desktop
/usr/share/metainfo/*.xml
/usr/share/icons/hicolor/*/*/*Macros de rutas
```

#### Macros de rutas.

| %{\_sysconfdir}         | /etc                                                      | <p><br></p>                                     |
| ----------------------- | --------------------------------------------------------- | ----------------------------------------------- |
| %{\_prefix}             | /usr                                                      | can be defined to /app for flatpak builds       |
| %{\_exec\_prefix}       | %{\_prefix}                                               | default: /usr                                   |
| %{\_includedir}         | %{\_prefix}/include                                       | default: /usr/include                           |
| %{\_bindir}             | %{\_exec\_prefix}/bin                                     | default: /usr/bin                               |
| %{\_libdir}             | %{\_exec\_prefix}/%{\_lib}                                | default: /usr/%{\_lib}                          |
| %{\_libexecdir}         | %{\_exec\_pre-fix}/libexec                                | default: /usr/libexec                           |
| %{\_sbindir}            | %{\_exec\_prefix}/sbin                                    | default: /usr/sbin                              |
| %{\_datadir}            | %{\_datarootdir}                                          | default: /usr/share                             |
| %{\_infodir}            | %{\_datarootdir}/info                                     | default: /usr/share/info                        |
| %{\_mandir}             | %{\_datarootdir}/man                                      | default: /usr/share/man                         |
| %{\_docdir}             | %{\_datadir}/doc                                          | default: /usr/share/doc                         |
| %{\_rundir}             | /run                                                      | <p><br></p>                                     |
| %{\_localstatedir}      | /var                                                      | <p><br></p>                                     |
| %{\_sharedstatedir}     | /var/lib                                                  | <p><br></p>                                     |
| %{\_lib}                | Lib64 / lib on 32bit platforms                            | <p><br></p>                                     |
| <p><br></p>             | <p><br></p>                                               | <p><br></p>                                     |
| %{\_dataroot-dir}       | %{\_prefix}/share                                         | default: /usr/share                             |
| %{\_var}                | /var                                                      | <p><br></p>                                     |
| %{\_tmppath}            | %{\_var}/tmp                                              | default: /var/tmp                               |
| %{\_usr}                | /usr                                                      | <p><br></p>                                     |
| %{\_usrsrc}             | %{\_usr}/src                                              | default: /usr/src                               |
| %{\_initddir}           | %{\_sysconfdir}/rc.d/init.d                               | default: /etc/rc.d/init.d                       |
| %{\_initrddir}          | %{\_initddir}                                             | antiguo error ortográfico, retro-compatibilidad |
| <p><br></p>             | <p><br></p>                                               | <p><br></p>                                     |
| %{buildroot}            | %{\_buildrootdir}/%{name}-%{version}-%{release}.%{\_arch} | same as $BUILDROOT                              |
| %{\_topdir}             | %{getenv:HOME}/rpmbuild                                   | <p><br></p>                                     |
| %{\_builddir}           | %{\_topdir}/BUILD                                         | <p><br></p>                                     |
| %{\_rpmdir}             | %{\_topdir}/RPMS                                          | <p><br></p>                                     |
| %{\_sourcedir}          | %{\_topdir}/SOURCES                                       | <p><br></p>                                     |
| %{\_specdir}            | %{\_topdir}/SPECS                                         | <p><br></p>                                     |
| %{\_srcrpmdir}          | %{\_topdir}/SRPMS                                         | <p><br></p>                                     |
| %{\_buildrootdir}       | %{\_topdir}/BUILDROOT                                     | <p><br></p>                                     |
| <p><br></p>             | <p><br></p>                                               | <p><br></p>                                     |
| %{\_kf5\_libdir}        | /usr/%{\_lib}                                             | <p><br></p>                                     |
| %{\_kf5\_configkcfgdir} | /usr/share/config.kcfg                                    | <p><br></p>                                     |
| <p><br></p>             | <p><br></p>                                               | <p><br></p>                                     |
| %{\_docdir}             | /usr/share/doc/packages                                   | <p><br></p>                                     |

#### Otras secciones

<pre><code><strong>// Si es openSUSE Leap 15.4 y 15.5 excluir paquete (arquitectura x86_64)
</strong><strong>
</strong><strong>%if 0%{?sle_version} == 150400 &#x26;&#x26; 0%{?is_opensuse} 
</strong>ExcludeArch: x86_64
%endif

%if 0%{?sle_version} == 150500 &#x26;&#x26; 0%{?is_opensuse} 
ExcludeArch: x86_64
%endif
</code></pre>

```
BuildRequires:  gcc-c++              // compilador de GNU para código escrito en C++
BuildRequires:  cmake                // herramienta de construcción para proyectos con CMakeList.txt
BuildRequires:  extra-cmake-modules  // añade los módulos, incluyendo los usados por find_package() en CMakeList.txt para encontrar el software.
BuildRequires:  fdupes               // herramienta para reemplazar los archivos duplicados por enlaces para disminuir el espacio usado en el sistema instalado
BuildRequires:  AppStream            // soporte de metadatos: /usr/share/metainfo/*.xml o mauimusic/org.kde.mauimusic.appdata.xml
```

```
%prep
%autosetup -p1                 // extrae mauimusic-0.1.0.tar.gz y entra en carpeta mauimusic-0.1.0
                               // autosetup -p1 -n maui-v0.1.0 especifica nombre carpeta si no coincide con %{name}-%{version}}
                               // -p1: omite nombre de la primera carpeta superior al aplicar patch

%build
%cmake_kf5 -d build            // configura
%cmake_build                   // compila

%install
%kf5_makeinstall -C build      // instala

%kf5_post_install
%fdupes %{buildroot}%{_prefix} // elimina duplicados reemplazandolos por enlaces
```
