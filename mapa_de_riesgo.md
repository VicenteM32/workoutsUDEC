# Mapa de riesgo del proyecto

**Grupo:** G01
**Integrantes:** Ignacio Soto, Leonardo Guerrero, Nicholas Garcia, Vicente Miranda
**Fecha:** 26-08-2026

Este archivo se completa en el taller de arqueología del proyecto (clase 3) y se
retoma en la clase 15 y en la clase 17, cuando se arme el plan de pruebas. Se
entrega completándolo en el repositorio del grupo, con un commit.

## Ronda 1: hallazgos en el código

Escala de la tercera columna: **directo** (apareció en la primera búsqueda),
**con vueltas** (hubo que abrir varios archivos antes), **no lo encontramos**.

| # | Pregunta | Archivo y línea | ¿Cuánto costó? | Lo que llama la atención |
|---|---|---|---|---|
| 1 | ¿Dónde se verifica la contraseña al iniciar sesión? |app/core/security.py linea 24 |directo | |
| 2 | ¿Cuánto dura un token de sesión antes de expirar? |app/core/config.py |directo |los 8 días se definen multiplicando las horas representadas como int |
| 3 | ¿Dónde guarda el navegador el token, y qué hace la aplicación ante un `401`? | | | |
| 4 | ¿Qué código HTTP devuelve la API si el token es inválido? ¿Y si es válido pero el usuario ya no existe? |app/api/endpoints/auth.py |medio |devuelve un HTTP_400_BAD_REQUEST en ambos casos. si el token es inválido: "Incorrect email or password" y si el usuario ya no existe: "Inactive user" |
| 5 | ¿Dónde se decide si alguien es administrador? |app/api/endpoints/dependencies.py | medio alto| el status code 400 es erroneo, funciona pero el más adecuado es el ERROR403|
| 6 | ¿Qué endpoints se pueden llamar sin estar autenticado? |app/api/endpoints/auth.py linea 16 |medio alto |se puede ingresar sin estar autenticado no entiendo por qué (checkar eso) |
| 7 | ¿Qué impide que dos personas modifiquen el mismo entrenamiento a la vez? |app/api/endpoints/workouts.py  linea 120 |medio |Hace get a la base de datos *db*. Esta parte no está del todo en el código, sino que es algo que falta |

"No lo encontramos" es un hallazgo válido: puede significar que no existe, y
también que el sistema es difícil de analizar.

## Ronda 2: riesgo por módulo

Impacto y probabilidad van de 1 a 5. El riesgo es el producto de ambos, y sirve
para ordenar los módulos, no para medir cuánto probar.

| Módulo | Impacto (1-5) | Probabilidad (1-5) | Riesgo | ¿Por qué? |
|---|---|---|---|---|
| Autenticación y tokens | | | | |
| Registro de entrenamientos | | | | |
| Base de datos de ejercicios | | | | |
| Plantillas de entrenamiento | | | | |
| Panel de administración | | | | |
| Historial y estadísticas | | | | |
| Interfaz responsive | | | | |

La columna del porqué es la única que se puede discutir: una justificación
nombra un usuario y una consecuencia.

## Ronda 3: si tuviéramos una sola tarde

Tres cosas, en orden de prioridad, con una frase de justificación cada una.

1. **...** *Porque ...*
2. **...** *Porque ...*
3. **...** *Porque ...*
