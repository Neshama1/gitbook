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

```
%define mauikit_version 3.0.1

Name:           mauimusic
Version:        0.1.0
Release:        0
License:        LGPL-3.0
Summary:        Discover and listen music
URL:            https://github.com/user/mauimusic
Source:         %{name}-%{version}.tar.gz

%if 0%{?sle_version} == 150400 && 0%{?is_opensuse} 
ExcludeArch: x86_64
%endif

%if 0%{?sle_version} == 150500 && 0%{?is_opensuse} 
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

%prep
%autosetup -p1

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

```

