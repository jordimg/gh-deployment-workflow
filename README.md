# GitHub Pages Deployment Workflow

## Descripción
Este proyecto demuestra cómo implementar una integración y despliegue continuo (CI/CD) utilizando **GitHub Actions** para desplegar automáticamente un sitio web estático en **GitHub Pages**.

El sitio web consiste en un simple archivo `index.html` que muestra el mensaje: _"Hello, GitHub Actions!"_. El despliegue solo se activará cuando se realicen cambios en `index.html` dentro de la rama `main`.

## Estructura del repositorio
```
.
├── .github/
│   ├── workflows/
│   │   ├── deploy.yml  # Archivo de configuración para GitHub Actions
├── index.html  # Página principal del sitio
├── README.md   # Documentación del proyecto
```

## Requisitos
1. Un repositorio en GitHub llamado **gh-deployment-workflow** (o un nombre similar).
2. Un archivo `index.html` con contenido básico.
3. Un archivo `deploy.yml` en `.github/workflows/` que contiene el workflow de GitHub Actions.
4. GitHub Pages habilitado en la configuración del repositorio.

## Configuración de GitHub Actions
El archivo `.github/workflows/deploy.yml` debe contener un flujo de trabajo para desplegar automáticamente el sitio en GitHub Pages.

Ejemplo de `deploy.yml`:
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main
    paths:
      - 'index.html'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Setup Pages
        uses: actions/configure-pages@v3

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: '.'

      - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v2
```

## Pasos para ejecutar el proyecto
1. **Clonar el repositorio:**
   ```sh
   git clone https://github.com/tu-usuario/gh-deployment-workflow.git
   ```
2. **Crear el archivo `index.html` con contenido:**
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>GitHub Actions</title>
   </head>
   <body>
       <h1>Hello, GitHub Actions!</h1>
   </body>
   </html>
   ```
3. **Crear el directorio de workflows y el archivo `deploy.yml`**
   ```sh
   mkdir -p .github/workflows
   nano .github/workflows/deploy.yml
   ```
   Copiar el contenido del workflow en el archivo.

4. **Subir los cambios al repositorio:**
   ```sh
   git add .
   git commit -m "Configuración inicial del despliegue en GitHub Pages"
   git push origin main
   ```

5. **Habilitar GitHub Pages en la configuración del repositorio:**
   - Ir a **Settings > Pages**
   - En "Source", seleccionar **GitHub Actions**

6. **Verificar la URL del sitio** después del despliegue exitoso:
   ```
   https://<tu-usuario>.github.io/gh-deployment-workflow/
   ```

## Stretch Goal: Mejorar con un Generador de Sitios Estáticos
Para hacer este proyecto más avanzado, puedes usar un generador de sitios estáticos como **Jekyll, Hugo o Astro** para crear un portafolio o blog más completo y automatizar su despliegue con GitHub Actions.

---
¡Listo! Ahora cada vez que actualices el `index.html` y hagas push a `main`, tu sitio en GitHub Pages se actualizará automáticamente. 🚀

