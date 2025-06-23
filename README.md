# Reutilización de Workflows

Basado en el ejercicio anterior, copiar el fichero 09-input-outputs.yml y empezar a trabajar a partir de el.

## Tareas 

1. **Hacer el flujo de trabajo `outputs.yml` reutilizable:**
   - renombrar el fichero a `o-workflow.yml` 
   - Agregar soporte para el evento `workflow_call` para que el flujo pueda ser llamado desde otros workflows, recibiendo parametros de entrada los inputs originales, y como parámetro de salida lo que imprime por consola el job deploy
   - Ajustar los inputs/outputs según sea necesario.

3. **Crear un flujo de trabajo llamado `caller-workflow.yml`:**
   - Tendrá como desencadente el evento `workflow_dispatch` con los siguientes inputs:
       - `dry-run`: booleano, valor predeterminado `false`, descripción: "Skip deployment and only print build output".
       - `target`: environment, requerido, descripción: "Which environment the workflow will target".       
   - Este flujo de trabajo debe de tener dos jobs:
       - `callToWd`: que llamará a `o-workflow.yml`, proporcionando los inputs que recibe el evento workflow_dispatch
       - `checkDeploying`: que se ejecutará solamente si el target es prod y salida del workflow llamado en el punto anterior empieza por 'Deploying', e imprimirá 'Check deploying Done' por consola


## Pruebas finales

1. Ejecutar el flujo `caller-workflow.yml` con diferentes combinaciones de valores para los inputs:
   - Ejemplo 1: `environment=int`, `dry-run=false`
   - Ejemplo 2: `environment=int`, `dry-run=true`
   - Ejemplo 3: `environment=prod`, `dry-run=true`

2. Observar el comportamiento del flujo reutilizable:
   - ¿Se ejecutan correctamente los trabajos `build` y `deploy` según los inputs proporcionados?

3. Reflexionar sobre los beneficios de usar workflows reutilizables:
   - Estandarización de procesos.
   - Reducción de duplicación de código.
   - Mayor mantenibilidad.

---


