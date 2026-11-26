# Resolución Reto 1 · Mi primer workflow: ¡hola, GitHub!

## Evidencias de ejecución
**Run fallido (rojo ❌):** https://github.com/JMRS92/cicd_nodejs_api/actions/runs/44518047889
**Run exitoso (verde ✅):** https://github.com/JMRS92/cicd_nodejs_api/actions/runs/44519411793

## Explicación

En sistemas operativos **Linux/Unix** y entornos de **CI/CD**, un código de salida distinto de cero (`exit 1`) indica que el proceso ha terminado de forma anormal debido a un error genérico, a diferencia del código `0`, que representa una ejecución exitosa.

Cuando un comando devuelve un código de error, GitHub Actions interpreta inmediatamente que el paso ha fallado, marca el job en rojo e interrumpe de forma automática la ejecución de los pasos posteriores (*fail-fast*).

---

# Resolución Reto 2 · Mi primera integración continua (CI)

## Enlace del workflows CI.yml

https://github.com/JMRS92/cicd_nodejs_api/actions/workflows/ci.yml

### 1. ¿Por qué `npm ci` usa el lockfile?

Garantiza una instalación **determinista y exacta**: instala estrictamente las versiones y hashes bloqueados en `package-lock.json`, asegurando que el entorno de CI sea 100% idéntico al local y evitando que se instalen versiones imprevistas.

### 2. ¿Por qué no debemos eliminar un test para conseguir un check verde?

Porque **enmascara el error en lugar de resolverlo**. Eliminar una prueba permite que código defectuoso pase a producción y destruye la red de seguridad contra futuros fallos (regresiones). Si falla, se corrige el código, no se borra el test.

### 3. ¿Qué pasa con los pasos siguientes si `lint` falla?

**Se cancelan automáticamente (_skipped_) y no se ejecutan**. Por defecto, ante un código de salida distinto de cero, GitHub Actions detiene de inmediato el job (_fail-fast_) para ahorrar tiempo y recursos de computación.

---

# Resolución Reto 3 · Ramas y pull requests: protege main

### 1. ¿En qué se diferencia un `push` en tu rama de fusionar a `main`?

* **Push en tu rama:** Sube tus cambios a un entorno de trabajo **aislado** en el repositorio remoto. No altera la rama principal ni afecta al trabajo del resto del equipo.
* **Fusionar a `main` (_merge_):** Integra el código en la rama troncal y definitiva del proyecto, incorporando los cambios a la versión oficial y estable que se despliega.

### 2. ¿Por qué es mejor evitar los cambios directos en producción?

* **Ausencia de red de seguridad:** Evita la ejecución de los controles automáticos de calidad del CI (linters, pruebas unitarias y de integración).
* **Riesgo de interrupción del servicio:** Un error de sintaxis o de lógica impacta de inmediato y de forma directa en los usuarios finales.
* **Pérdida de revisión y trazabilidad:** Se prescinde de la revisión por pares (_code review_) y se complica el rastreo o la reversión ágil de versiones en caso de incidentes.
