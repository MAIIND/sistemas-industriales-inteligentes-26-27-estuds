# Cómo preparar tu entorno de Python para el curso

*Sistemas Industriales Inteligentes (MAIIND)*

Esta guía te lleva paso a paso a tener listo un entorno de Python propio para la asignatura y a usarlo en Visual Studio Code. No hace falta saber programar para seguirla: basta con copiar y pegar las órdenes.

Usaremos Visual Studio Code. Si no lo tienes, comienza por descargar la versión adecuada
para tu sistema operativo desde **https://code.visualstudio.com/**. Después prepara
Python y el entorno siguiendo los pasos de esta guía.

**¿Qué es un "entorno virtual" y por qué lo usamos?** Es una copia aislada de Python, con sus propias librerías, que vive dentro de la carpeta de tu proyecto. Así, lo que instales para esta asignatura no interfiere con otros proyectos ni con el Python del sistema, y todos trabajamos con las mismas versiones. Es una práctica estándar y muy recomendable.

---

## Requisito previo: tener Python instalado

Comprueba si ya lo tienes. Abre una terminal y escribe:

```
python --version
```

Si no funciona, prueba con `python3 --version`. Para la instalación básica de S1
(opción B del paso 4) se puede utilizar Python 3.10 o superior. Si vas a instalar las
versiones fijadas de todo el curso (opción A), necesitas **Python 3.12 o superior**:
algunas dependencias no admiten 3.10 ni 3.11. La versión comprobada en el equipo del
docente es **Python 3.13.9**; si preparas un entorno nuevo para todo el curso, usa 3.13.

Si no está instalado, descárgalo de **https://www.python.org/downloads/** e instálalo.

> **Importante en Windows:** durante la instalación, marca la casilla **"Add Python to PATH"** antes de pulsar "Install". Es fácil pasarla por alto y luego da problemas.

**¿Dónde está la terminal?**
- **Windows:** busca "PowerShell" o "Símbolo del sistema" en el menú de inicio.
- **macOS:** busca "Terminal" en Spotlight (Cmd + Espacio).
- **Linux:** tu terminal habitual.

---

## Paso 1 — Crear la carpeta del curso

Obtén la carpeta `SII` siguiendo la [guía de Git y GitHub](guia_git_github_alumnado.md):
clona el repositorio de materiales del profesor y conecta tu repositorio personal.
Si ya has completado ese paso, utiliza esa misma carpeta. Dentro, los cuadernos
de cada semana van en su subcarpeta (`semana-01`, `semana-02`…) y los datos en una
subcarpeta común `datasets`:

```
SII/
├── docs/
│   └── requirements.txt
├── datasets/
│   └── dataset_flotacion_mini.csv
└── semana-01/
    ├── Semana1_Python_minimo.ipynb
    └── Semana1_ALUMNO.ipynb
```

Puedes preparar los datos de todo el curso descargando los recursos disponibles en
[la carpeta de Google Drive](https://drive.google.com/drive/folders/1UVhDdCW6bLvXU8L0BaK7CulrtUaVzeT-?usp=sharing).
Copia su contenido directamente en `SII/datasets/`, conservando los nombres de los
archivos y las subcarpetas. Para la práctica de S1 basta `dataset_flotacion_mini.csv`,
que debes descargar por separado y guardar en esa carpeta. El repositorio de
[materiales del alumnado](https://github.com/MAIIND/sistemas-industriales-inteligentes-26-27-estuds)
contiene `semana-01/` y `docs/`; las nuevas semanas se incorporan con `git pull`.
No necesitas esperar a que terminen todas las descargas de datos para empezar.
El inventario disponible para estudiantes está en `datasets/README.txt`.

**Respeta esta estructura y los nombres de las carpetas.** Los cuadernos buscan los datos con rutas como `../datasets/dataset_flotacion_mini.csv` ("sube un nivel desde la carpeta de la semana y entra en `datasets`"). Si pones el CSV junto al cuaderno, verás un `FileNotFoundError`. Si descargas el repositorio completo del curso, ya viene con esta estructura.

Desde la terminal, sitúate dentro de la carpeta `SII`:

```
cd ruta/a/tu/carpeta/SII
```

(Sustituye `ruta/a/tu/carpeta/SII` por la ruta real. Un truco: en VS Code puedes abrir la carpeta y usar su terminal integrada, que ya se sitúa dentro.)

---

## Paso 2 — Crear el entorno virtual

Dentro de la carpeta, ejecuta:

```
python -m venv .venv
```

(Si en tu sistema `python` no funciona, usa `python3`.)

Esto crea una subcarpeta llamada `.venv` con tu Python aislado. Solo hay que hacerlo **una vez** por proyecto.

---

## Paso 3 — Activar el entorno

Activar el entorno le dice a la terminal que use el Python de `.venv`. La orden depende de tu sistema:

**Windows (PowerShell):**
```
.venv\Scripts\Activate.ps1
```

**Windows (Símbolo del sistema / CMD):**
```
.venv\Scripts\activate.bat
```

**macOS y Linux:**
```
source .venv/bin/activate
```

Si funciona, verás que al principio de la línea de la terminal aparece `(.venv)`. Eso indica que el entorno está activo.

> **Problema frecuente en Windows (PowerShell):** si sale un error de "ejecución de scripts está deshabilitada", ejecuta una vez esta orden y vuelve a intentar la activación:
> ```
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```

Para **desactivar** el entorno cuando termines, escribe simplemente:
```
deactivate
```

---

## Paso 4 — Instalar las librerías

Con el entorno **activado** (tienes que ver `(.venv)` en la terminal) y la terminal
situada en **SII**, elige una de estas dos opciones.

El archivo **`docs/requirements.txt`**, incluido en el repositorio, contiene la lista de
librerías del curso y sus versiones fijadas. Puedes pedir a `pip` que instale esa
lista completa, en lugar de escribir los nombres uno por uno.

**Opción A — entorno completo del curso, con versiones fijadas** (Python 3.12 o superior;
entorno verificado con 3.13.9). Ejecuta desde **SII**:
```bash
python -m pip install -r docs/requirements.txt
```

La opción **`-r`** indica que `pip` debe leer las dependencias del archivo que viene
a continuación. Mantén `requirements.txt` dentro de `docs/`, tal como viene en el
repositorio.

**Opción B — instalación básica para S1** (suficiente para la práctica y los ejemplos
de Python mínimo; sin instalar aún todas las dependencias del curso):
```
python -m pip install numpy pandas matplotlib jupyter ipykernel
```

Si empiezas con la opción B, más adelante puedes completar el mismo entorno con
la orden de la opción A, desde **SII** y con `.venv` activado.

Puede tardar varios minutos según la conexión y el equipo, especialmente la opción A.
Solo hay que hacerlo una vez, o cuando se añada alguna librería nueva. La opción A fija
las versiones; la B prepara los paquetes básicos con las versiones compatibles que
resuelva pip.

Para comprobar que se instaló bien:
```
python -c "import pandas, numpy, matplotlib; print('Todo correcto')"
```

---

## Paso 5 — Preparar Visual Studio Code

1. Si no lo tienes, descarga VS Code de **https://code.visualstudio.com/** e instálalo.
2. Abre VS Code y, en el panel de **Extensiones** (el icono de cuadraditos a la izquierda, o `Ctrl+Shift+X`), instala estas dos extensiones de Microsoft:
   - **Python**
   - **Jupyter**
3. Instala también **Rainbow CSV** (autor: *mechatroner*). Colorea cada columna de un fichero `.csv` para que se lea con facilidad, y su comando **Rainbow CSV: Align columns** (en la paleta de comandos, ver Paso 6) las alinea como una tabla. No es obligatoria, pero ayuda mucho a echar un primer vistazo a los datos.
4. Abre la carpeta del curso: menú **Archivo → Abrir carpeta…** y elige tu carpeta `SII` (la carpeta raíz, no `semana-01`).

---

## Paso 6 — Decirle a VS Code que use tu entorno

Aquí está la clave: hay que indicarle a VS Code que trabaje con el Python de `.venv`, no con otro.

1. Abre la **paleta de comandos** con `Ctrl+Shift+P` (en Mac, `Cmd+Shift+P`).
2. Escribe **`Python: Select Interpreter`** y púlsalo.
3. En la lista, elige el que apunta a tu carpeta `.venv` (suele aparecer como *Recommended* y con la ruta `.venv`).

A partir de ahora, VS Code usará ese entorno.

---

## Paso 7 — Abrir un cuaderno y elegir el "kernel"

1. En el explorador de archivos de VS Code (a la izquierda), haz doble clic en el cuaderno `.ipynb`.
2. Arriba a la derecha del cuaderno verás un botón para **seleccionar el kernel** (puede poner "Select Kernel" o mostrar un nombre de Python). Púlsalo.
3. Elige **Python Environments…** y luego tu entorno **`.venv`**.

El "kernel" es el Python que ejecutará las celdas del cuaderno. Debe ser el de `.venv` para que encuentre las librerías que instalaste.

---

## Paso 8 — Comprobar que todo funciona

En el cuaderno, sitúate en la primera celda de código y ejecútala con **`Shift + Enter`**. Si no da error y puedes ir ejecutando celdas, ¡ya está todo listo!

Prueba rápida: crea una celda con esto y ejecútala:

```python
import pandas as pd
print("pandas versión", pd.__version__)
```

Si imprime la versión sin errores, tu entorno está correctamente configurado.

---

## Uso en el día a día

Una vez configurado, no repites la instalación. Tu rutina será:

- **En la terminal** (si trabajas desde ella): entra en la carpeta y activa el entorno (Paso 3) antes de trabajar; `deactivate` al terminar.
- **En VS Code:** normalmente recuerda tu elección. Solo asegúrate de que el cuaderno tiene seleccionado el kernel `.venv` (arriba a la derecha). La terminal integrada de VS Code activa el entorno automáticamente al abrirla.

---

## Problemas frecuentes

- **"python no se reconoce como un comando"** → Python no está en el PATH. En Windows, reinstala marcando "Add Python to PATH". O prueba con `py` en lugar de `python`.
- **No aparece `.venv` en la lista de intérpretes de VS Code** → cierra y vuelve a abrir VS Code con la carpeta del curso abierta; el `.venv` debe estar dentro de esa carpeta.
- **Al ejecutar una celda dice que no encuentra `pandas` (u otra librería)** → casi siempre es que el cuaderno está usando otro kernel. Revisa el kernel arriba a la derecha y selecciona el `.venv`. Comprueba también que instalaste las librerías con el entorno activado.
- **`Could not open requirements file`** → sitúa la terminal en `SII` y comprueba que existe `SII/docs/requirements.txt`. La orden es `python -m pip install -r docs/requirements.txt`.
- **`FileNotFoundError: ../datasets/dataset_flotacion_mini.csv`** → el CSV no está donde lo busca el cuaderno. Revisa la estructura del Paso 1: el cuaderno en `SII/semana-01/` y el CSV en `SII/datasets/`. No cambies la ruta del cuaderno; mueve el fichero.
- **En PowerShell no deja activar el entorno** → aplica la orden `Set-ExecutionPolicy` del Paso 3.
- **Tengo `python3` pero no `python`** (típico en Mac/Linux) → usa `python3` en las órdenes de creación del entorno; una vez activado, dentro del entorno `python` ya funciona.
