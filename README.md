# Ejercicio: Reutilizando la lógica de construcción con Workflows

##  Objetivo

Aprender a reutilizar workflows en GitHub Actions. El objetivo es mover la lógica del job `build` a un flujo reutilizable y dejar que un flujo principal se encargue de ejecutar el despliegue en función del resultado de la construcción.

---

##  Tareas

### 1. Adaptar el workflow `outputs.yml`

El archivo `.github/workflows/outputs.yml` ya existe y contiene la lógica de construcción.

Debes modificarlo para que sea reutilizable:

- Renombra el archivo a `.github/workflows/o-workflow.yml` (si es necesario).
- Sustituye el `on: workflow_dispatch` por `on: workflow_call`.
- Acepta un input llamado `build-status` de tipo `string` (por ejemplo: `success` o `failure`).
- Exporta como **output** el valor `status` generado por el job `build`.

> 💡 Este workflow se reutilizará desde otro.

---

### 2. Crear el flujo principal

Crea un nuevo archivo llamado `.github/workflows/main-deploy.yml` con la siguiente funcionalidad:

- Se activa con `workflow_dispatch` y recibe un input:
  - `build-status` (choice: `success`, `failure`, default: `success`)
- Tiene dos jobs:
  1. `call-build`: llama al workflow `o-workflow.yml`, pasándole el input `build-status`.
  2. `deploy`: se ejecuta solo si el output `status` del job anterior es `'success'`.

---

##  Pruebas

Ejecuta el flujo principal desde la interfaz de GitHub (UI):

- ✅ Si el input es `success` → se debe ejecutar el job `deploy`.
- ❌ Si el input es `failure` → el job `deploy` no debe ejecutarse.

---

##  Reflexión

- ¿Qué beneficios aporta el uso de workflows reutilizables?
- ¿Cómo facilita esto la estandarización de procesos?

