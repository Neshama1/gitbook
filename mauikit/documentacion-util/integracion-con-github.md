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
git clone https://github.com/user/mauimusic.git
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

###

### 6. Cree el toke de acceso a GitHub.

GitHub > Dashboard >  pulse sobre la imagen de perfil (superior derecha) > Settings > Developer settings > Personal access tokens > Tokens (classic) > Generate new token (classic)

* Note: GitHub Token
* Expiration: No expiration
* Scopes: todos
* Generate token
* Copie el nuevo token. No podrá verlo de nuevo, por lo que debe guardarlo.

### 7. Cree un token en Open Build Service.

Your Home Project > pulse sobre la imagen de perfil (superior derecha) > Your profile > Manage Your Tokens > Create Token >&#x20;

* Type: workflow
* Description: OBS Personal Access Token
* SCM Token: pega el token de GitHub obtenido en el punto 6.
* Path for Workflows Configuration File (no modificar): .obs/workflows.yml
* Create

Apunte su OBS Personal Access Token:

* Secret: Copie y guarde.
* Token trigger url: Copie y guarde.

### 8. Cree en GitHub un webhook para su aplicación.

Seleccione:

* GitHub > click sobre imagen de perfil (superior derecha) > Your repositories > su aplicación (mauimusic)
* De las opciones superiores (code, Issues, Pull requests...) seleccione: Settings > Webhooks > Add webhook
  * Payload URL: Pegar su "Token trigger url" del punto 7.
  * Content type: application json
  * Secret: Pegar su "Secret" del punto 7.
  * Seleccione: Send me everything.
  * Add webhook.

### 9. Crear .obs/workflows.yml

* Abra la página de código de su aplicación (mauimusic): Selecciones Code o click sobre imagen de perfil (superior derecha) > Your repositories > su aplicación (mauimusic).
* Add file > Create new file
  * Pegar en la caja de texto "mauimusic/Name your file". Sustituya Name your file por: .obs/workflows.yml
  * Creará la carpeta oculta ".obs" y el archivo workflows.yml a la vez.

Incluya como contenido de workflows.yml:

```
rebuild_master:
    steps:
        - rebuild_package:
            project: home:usuario:subproyecto1
            package: mauimusic
    filters:
    event: push
workflow:
  steps:
    - branch_package:
        source_project: home:usuario
        source_package: mauimusic
        target_project: home:usuario:subproyecto2
  filters:
    event: tag_push 
```

En el archivo anterior se ha incluido:

* rebuild\_master: para compilar cada commit en subproyecto1 y paquete mauimusic.
* workflow: para compilar cada nueva publicación de versión o tag de su aplicación en subproyecto2 y paquete mauimusic.

Haga clic en Commit changes > Commit changes.

### 10. Descarge los cambios a su carpeta local:

```
cd /home/user/Devel/Apps/mauimusic
git pull
```

