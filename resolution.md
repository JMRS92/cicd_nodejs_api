# Resolución Reto 1

## Enlace run (rojo) fallido:

https://github.com/JMRS92/cicd_nodejs_api/actions/runs/44518047889

## Enlace run (verde) Ok:

https://github.com/JMRS92/cicd_nodejs_api/actions/runs/44519411793

## Explicación de las dos frases:

En sistemas operativos Linux/Unix y entornos de CI/CD, un código de salida distinto de cero (exit 1) indica que el proceso ha terminado de forma anormal debido a un error genérico, a diferencia del código 0 que representa una ejecución exitosa.

Cuando un comando devuelve este código, GitHub Actions interpreta que el paso ha fallado, marca el job en rojo y detiene automáticamente la ejecución de los pasos posteriores.
