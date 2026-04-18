# techmaster-central-devops
1. README para el Repositorio Central
Ruta: techmaster-central-devops/README.md

Markdown
# 🛠️ TechMaster Central DevOps

Este repositorio actúa como el núcleo de infraestructura de **TechMaster LTDA**, proporcionando flujos de trabajo (Workflows) estandarizados y reutilizables para toda la organización.

## 📋 Descripción
Contiene plantillas de CI/CD basadas en **GitHub Actions** que permiten unificar los criterios de calidad, seguridad y despliegue en todos los microservicios de la empresa.

## 🚀 Componentes Reutilizables

### Plantilla de Construcción Docker (`plantilla-docker.yml`)
Flujo de trabajo centralizado que maneja el ciclo de vida completo de una imagen:
* **Validación:** Instalación de dependencias y ejecución de pruebas unitarias.
* **Build:** Construcción de la imagen utilizando Docker Buildx.
* **Push (Condicional):** Publicación en Docker Hub controlada por parámetros.

## ⚙️ Uso
Para consumir este flujo, el repositorio cliente debe invocarlo mediante `uses:`:

```yaml
uses: carlcuevas/techmaster-central-devops/.github/workflows/plantilla-docker.yml@main
with:
  publicar_imagen: true/false
🛡️ Seguridad
Las credenciales de acceso al registro de contenedores nunca se almacenan en este repositorio, se reciben como secretos cifrados desde el repositorio cliente.


---

## 2. README para el Repositorio Cliente
**Ruta:** `techmaster-api-cliente/README.md`

```markdown
# 📦 TechMaster API Cliente

Repositorio de aplicación para TechMaster LTDA. Implementa una arquitectura de pipelines desacoplados consumiendo recursos del repositorio central de DevOps.

## 🚀 Arquitectura CI/CD
Este proyecto implementa dos flujos de trabajo independientes para garantizar la estabilidad del software:

### 1. Validación Continua (CI)
* **Trigger:** Push en ramas `feature/*`.
* **Propósito:** Validar cambios sin afectar el registro de producción.
* **Acciones:** Ejecuta `npm test` y construye la imagen Docker para verificar la integridad del Dockerfile. **No publica** en Docker Hub.

### 2. Despliegue de Release (CD)
* **Trigger:** Creación de etiquetas de versión (Tags) `v*.*.*`.
* **Propósito:** Publicar versiones oficiales y estables.
* **Acciones:** Ejecuta pruebas, construye la imagen y la publica automáticamente en **Docker Hub**.

## 🛠️ Tecnologías
* **Backend:** Node.js / Express
* **Infraestructura:** Docker / GitHub Actions
* **Registry:** Docker Hub (`ttzeta00/auy1104-api-cliente`)

## 🔑 Configuración de Secretos
Para que los pipelines funcionen, se deben configurar los siguientes *Repository Secrets* en GitHub:
* `DOCKERNICK`: Usuario de Docker Hub.
* `DOCKERCONTRA`: Access Token de Docker Hub.

## 📄 Autor
* **Carlos Rodrigo Cuevas** - *DevOps Engineer - TechMaster LTDA*
