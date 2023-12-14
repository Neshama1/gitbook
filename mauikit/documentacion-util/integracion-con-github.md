---
description: >-
  Open Build Service de openSUSE puede interactuar con GitHub, obteniendo y
  compilando el código fuente de cada commit o cada nueva publicación de versión
  o tag.
---

# Integración con GitHub

### 1. Cree una cuenta en GitHub.

### 2. Cree un repositorio (su aplicación): GitHub > Dashboard > + > New repository.

* Repository name: mauimusic
* Marque: Add a README file
* Eliga una licencia

### 3. Clone su repositorio en su carpeta de desarrollo. Si ya tiene un código preexistente haga copia del contenido a la nueva carpeta clonada:

```
cd /home/user/Devel/Apps
git clone https://github.com/Neshama1/mauimusic.git
```

### 4. Instale y haga login en GitHub:

```
sudo zypper install gh openssh-askpass-gnome
gh auth login
```

Seleccione:

* GitHub.com > HTTPS > Autenticate Git with your GitHub credentials > Login with a web browser.
* Copie el código de autenticación.
* Presione tecla Enter.
* Ingrese usuario y contraseña de GitHub
* Pege el código de autenticación.
* Clic botón Authorize github.

Configure su correo y nombre:

```
git config --global user.mail "tucorreo@servidor.com
git config --global user.name "tu nombre"
```

### 5. Haga su primer commit con el nuevo contenido:

```
cd /home/user/Devel/Apps/mauimusic
git add *
git commit -m "first commit"
git push origin main
```

#### &#x20;&#x20;
