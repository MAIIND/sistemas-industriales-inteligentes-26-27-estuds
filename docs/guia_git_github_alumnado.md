# Git y GitHub: descargar y actualizar los materiales

*Sistemas Industriales Inteligentes · MAIIND · Curso 2026–2027*

Los materiales se publican en
[el repositorio de la asignatura](https://github.com/MAIIND/sistemas-industriales-inteligentes-26-27-estuds).
Cada estudiante organiza sus archivos locales como prefiera.
**Las entregas se realizan por archivos en el Campus Virtual.**

## 1. Comprueba que tienes Git

Abre una terminal y ejecuta:

```bash
git --version
```

Si aparece una versión, continúa. Si el comando no se reconoce, instala
[Git para tu sistema](https://git-scm.com/downloads), vuelve a abrir la terminal
y repite la comprobación.

## 2. Clona los materiales una vez

El repositorio será público. Para descargarlo y actualizarlo por HTTPS **no necesitas
cuenta de GitHub ni autenticarte**.

Sitúa la terminal en la carpeta donde guardarás el curso y ejecuta:

```bash
git clone https://github.com/MAIIND/sistemas-industriales-inteligentes-26-27-estuds.git
```

Se crea una carpeta llamada `sistemas-industriales-inteligentes-26-27-estuds`.
Si ya existe otra con ese nombre y trabajo previo, elige otra ubicación y conserva
tus archivos.

## 3. Recibe nuevas semanas y correcciones

Abre una terminal dentro de `sistemas-industriales-inteligentes-26-27-estuds` y ejecuta:

```bash
git pull --ff-only
```

Revisa los materiales actualizados y ten en cuenta las correcciones del profesor
en tu trabajo. Si tus cambios locales impiden actualizar, conserva tus
archivos y gestiona la actualización según tu flujo de trabajo; no descartes
respuestas para forzar la descarga.
