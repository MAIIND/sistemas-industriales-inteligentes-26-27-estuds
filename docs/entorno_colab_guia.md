# Semana 1 en Google Colab

*Sistemas Industriales Inteligentes (MAIIND) · guía para estudiantes*

Esta es una forma opcional de hacer la práctica de la semana 1 desde el navegador. Necesitas una cuenta de Google, el cuaderno `Semana1_ALUMNO.ipynb` y el fichero `dataset_flotacion_mini.csv`. Para esta práctica basta el entorno de Python que trae Colab; no necesitas instalar las dependencias de todo el curso ni activar una GPU.

**Tiempo de preparación:** unos 5–10 minutos, más el tiempo de trabajo en el cuaderno.

## 1. Descarga los dos ficheros

Descarga estos ficheros y guárdalos en tu ordenador, **sin cambiar sus nombres**:

- [`Semana1_ALUMNO.ipynb`](../semana-01/Semana1_ALUMNO.ipynb), del repositorio de materiales del alumnado (carpeta `semana-01/`). Si lo abres en GitHub, utiliza **Download raw file** para descargar el cuaderno.
- `dataset_flotacion_mini.csv` (unos 4,5 MB), de la [carpeta de datos de Google Drive](https://drive.google.com/drive/folders/1UVhDdCW6bLvXU8L0BaK7CulrtUaVzeT-?usp=sharing), como indica el [paso 1 de la guía local](entorno_python_vscode_guia.md#paso-1--crear-la-carpeta-del-curso). Los datos se descargan por separado de los materiales.

No hace falta descargar el CSV crudo completo de la planta. El cuaderno de la semana 1 trabaja con el subconjunto pequeño.

## 2. Abre y guarda tu copia del cuaderno

1. Entra en [Google Colab](https://colab.research.google.com/) e inicia sesión.
2. Elige **Archivo → Subir cuaderno** y selecciona `Semana1_ALUMNO.ipynb`. Si la ventana de inicio muestra la pestaña **Subir**, también puedes usarla.
3. Elige **Archivo → Guardar una copia en Drive** para tener tu propia copia editable. Ponle un nombre reconocible, por ejemplo `Semana1_Apellido.ipynb`.

Trabaja siempre en tu copia. El cuaderno conserva el texto, el código y las salidas que guardes; los ficheros que subas a la máquina temporal de Colab requieren otro paso para conservarse.

## 3. Prepara el CSV antes de ejecutar la práctica

En el cuaderno, inserta **una celda de código nueva antes de la primera celda de código** (la que empieza por `import pandas as pd`). Pega y ejecuta esto:

```python
from pathlib import Path
import os
from google.colab import files

subidos = files.upload()  # Selecciona dataset_flotacion_mini.csv de tu ordenador
nombre = "dataset_flotacion_mini.csv"
assert nombre in subidos, f"Selecciona exactamente {nombre}"

carpeta_datos = Path("/content/datasets")
carpeta_datos.mkdir(exist_ok=True)
(carpeta_datos / nombre).write_bytes(subidos[nombre])

Path("/content/semana-01").mkdir(exist_ok=True)
os.chdir("/content/semana-01")
print("Carpeta de trabajo:", Path.cwd())
print("CSV disponible:", Path("../datasets/dataset_flotacion_mini.csv").is_file())
```

Cuando Colab te pida un fichero, selecciona el CSV descargado en el paso 1. Al final debes ver `CSV disponible: True`.

El cuaderno usa rutas como `../datasets/dataset_flotacion_mini.csv`: la celda crea las carpetas necesarias y sitúa la ejecución en `semana-01`. **No cambies `FICHERO` ni las rutas del ejercicio.**

## 4. Trabaja en el cuaderno

Ejecuta las celdas de arriba abajo con el botón **▶** o con **Mayús + Intro**. Completa los apartados `TODO` de `Semana1_ALUMNO.ipynb` y vuelve a ejecutar cada celda que edites. Si una celda usa una variable creada antes, primero ejecuta las anteriores.

Como comprobación inicial, la celda con `FICHERO` debe poder leer el CSV sin `FileNotFoundError`. En la sección 4 guardarás tu tabla horaria en `../datasets/flotacion_horaria_mini.csv`.

## 5. Conserva el resultado

Después de ejecutar la celda `tabla.to_csv(...)` de la sección 4, añade y ejecuta esta celda al final del cuaderno para descargar el CSV generado:

```python
from pathlib import Path
from google.colab import files

salida = Path("../datasets/flotacion_horaria_mini.csv")
assert salida.is_file(), "Ejecuta primero la celda que guarda la tabla horaria"
files.download(str(salida))
```

El navegador descargará `flotacion_horaria_mini.csv`. Consérvalo junto con tu copia del cuaderno; sigue las instrucciones del docente sobre qué archivo entregar. Comprueba que la copia del cuaderno aparece en tu Google Drive antes de cerrar la pestaña.

Para entregar, descarga también tu copia del cuaderno desde
**Archivo → Descargar → Descargar .ipynb** y súbela al Campus Virtual junto con
los archivos que pida el enunciado. Guardarla en Drive no realiza la entrega.
Si además la conservas en tu ordenador, organiza tus archivos como prefieras;
mantén las rutas de datos necesarias si vuelves a ejecutarla localmente.

## Si vuelves otro día

Abre tu cuaderno desde Google Drive. Colab puede darte una máquina de ejecución nueva: vuelve a ejecutar **primero la celda de preparación del paso 3** y después las celdas de la práctica en orden. Si ya habías descargado `flotacion_horaria_mini.csv`, tu copia local sigue disponible aunque la máquina anterior haya desaparecido.

## Problemas habituales

| Qué ves | Qué hacer |
|---|---|
| `FileNotFoundError: ../datasets/dataset_flotacion_mini.csv` | Ejecuta otra vez la celda del paso 3, sube el CSV correcto y comprueba que imprime `CSV disponible: True`. |
| `NameError` para una variable del cuaderno | Ejecuta las celdas anteriores en orden; Colab puede haber reiniciado la sesión. |
| La descarga dice que no existe `flotacion_horaria_mini.csv` | Completa y ejecuta primero la celda `tabla.to_csv(...)` de la sección 4. |
| No aparece el trabajo al volver | Abre la **copia guardada en Drive**, no el cuaderno original que descargaste. |

Colab usa máquinas temporales: el cuaderno puede estar guardado en Drive mientras que un CSV subido a `/content` ya no está. [Ayuda oficial de Colab sobre cuadernos, archivos y sesiones](https://research.google.com/colaboratory/intl/es/faq.html).
