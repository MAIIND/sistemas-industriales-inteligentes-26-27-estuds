# Sistemas Industriales Inteligentes · MAIIND · 2026–2027

Materiales para estudiantes de la Universidad de Oviedo. El curso desarrolla un
sensor virtual de sílice a partir de datos reales de flotación de mineral de hierro.
Las semanas se publican progresivamente en este repositorio.

## Empezar

1. Sigue la [guía de Git y GitHub](docs/guia_git_github_alumnado.md) para clonar los
   materiales en tu equipo y recibir las nuevas semanas y correcciones.
2. Prepara [Python y VS Code](docs/entorno_python_vscode_guia.md). Usa la instalación
   básica para S1 o las versiones del curso en `docs/requirements.txt`.
3. Consulta [los datos de S1](datasets/README.txt) y descarga
   `dataset_flotacion_mini.csv` en `SII/datasets/`.
4. Abre [la semana 1](semana-01/README.md) y sigue la secuencia de clase.

Si una incidencia impide trabajar en local, utiliza la [guía de Colab](docs/entorno_colab_guia.md).

## Material disponible

| Material | Uso |
|---|---|
| [Presentación general](presentacion-curso/curso.pdf) | Estructura, evaluación, caso industrial y recorrido técnico de consulta |
| [Semana 1](semana-01/README.md) | Herramientas, datos del proyecto y práctica guiada |
| [Semana 2: diapositivas de regresión lineal](<semana-02/Semana2_Conceptos Basicos de Aprendizaje Supervisado (Regresion Lineal).pdf>) | Conceptos básicos de aprendizaje supervisado |
| [Semana 2: cuaderno de prácticas](semana-02/Semana2_ALUMNO.ipynb) | Regresión, descenso de gradiente, validación y regularización con datos sintéticos |
| [Descripción del proceso y dataset](docs/descripcion_dataset_flotacion.md) | Referencia para interpretar las variables |

## Trabajo y actualizaciones

Desde `SII`, `git pull --ff-only` recibe los nuevos materiales del profesor.
Cada estudiante gestiona sus archivos locales y su versionado como prefiera.
Revisa los materiales actualizados y ten en cuenta las correcciones del profesor
en tu trabajo.

Conserva las carpetas `semana-01/`, `docs/` y `datasets/` al mismo nivel. Los
cuadernos cargan los datos desde su semana mediante rutas `../datasets/`.
Entrega los archivos solicitados en el Campus Virtual, donde también se publican
las calificaciones. S1 es nivelación: no tiene presentación del alumnado ni defensa oral.

## Evaluación y licencia

10 % trabajo continuo, 40 % examen y 50 % proyecto final. La primera tarea formal
es la de S2, cuya defensa corresponde al comienzo de S3.

Material docente de Antonio Miguel López Rodríguez, bajo
[CC BY-NC-SA 4.0](LICENSE). Los datasets conservan su procedencia y licencia propias.
