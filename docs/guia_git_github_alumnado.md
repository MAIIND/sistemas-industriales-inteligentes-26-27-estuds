# Git y GitHub: recibir materiales y subir tu trabajo

*Sistemas Industriales Inteligentes · MAIIND · Curso 2026–2027*

Esta guía explica cómo descargar los materiales del profesor, recibir las nuevas
semanas y subir tus cuadernos a un repositorio propio de GitHub. Debes dar acceso
al profesor para que pueda revisar tu trabajo.

## 1. Qué vas a utilizar

Trabajarás en **una sola carpeta local**, llamada `SII`, conectada con dos
repositorios de GitHub:

| Nombre en Git | A qué repositorio apunta | Para qué se utiliza |
|---|---|---|
| `upstream` | Materiales del profesor | Descargar nuevas semanas y correcciones |
| `origin` | Tu repositorio personal | Subir tus ejercicios y avances |

Un **repositorio** guarda archivos y su historial de cambios. Un **remoto** es una
dirección de otro repositorio. Un **commit** guarda una versión de tu trabajo en tu
ordenador; un **push** la sube a GitHub; un **pull** incorpora cambios de un remoto.

El profesor publica los cuadernos base. Tú los modificas dentro de su carpeta de
semana y guardas las respuestas en tu repositorio. Con la configuración de esta
guía, **`git pull` recibe los materiales del profesor y `git push` sube tu trabajo
a tu repositorio**. Git permite configurar destinos distintos para ambas operaciones.
[Referencia: configuración de remotos de Git](https://git-scm.com/docs/git-config#Documentation/git-config.txt-branchnamepushRemote).

Esta guía se refiere a un repositorio personal por estudiante y a la rama `main`.
Si el profesor organiza trabajo en grupo, indicará cómo sincronizar también los
cambios de los compañeros.

## 2. Antes de empezar

Necesitas una cuenta en [GitHub](https://github.com/), Git instalado y Visual Studio
Code. Puedes descargar Git desde [su página oficial](https://git-scm.com/downloads).
Después de instalarlo, vuelve a abrir la terminal y comprueba:

```bash
git --version
```

Los comandos se escriben en la terminal integrada de VS Code: **Terminal → Nueva
terminal**. Ejecuta cada línea por separado y revisa su resultado antes de seguir.

El repositorio de materiales de la asignatura y la cuenta docente son:

| Dato | Dirección |
|---|---|
| URL del repositorio de materiales para estudiantes | `https://github.com/MAIIND/sistemas-industriales-inteligentes-26-27-estuds.git` |
| Correo de GitHub del profesor, para invitarlo | `amlopez@uniovi.es` |

`MAIIND` es la organización que aloja los materiales; la invitación de revisión se
envía al profesor mediante el correo `amlopez@uniovi.es`.

Sustituye `TU_USUARIO` por tu usuario de GitHub. **Los marcadores de usuario son
ejemplos: reemplázalos por los datos reales antes de ejecutar los comandos.**
Los pasos siguientes suponen que el repositorio de materiales tiene una rama `main`.

### Identificar tus commits

Configura una vez tu nombre y tu correo:

```bash
git config --global user.name "Tu nombre y apellidos"
git config --global user.email "tu-correo-de-commits"
```

Sustituye ambos ejemplos. Puedes utilizar el correo de commits que GitHub muestra
en **Settings → Emails**, incluida la dirección `noreply` de tu cuenta. Estos datos
identifican la autoría de tus commits; no sirven para iniciar sesión.

### Autenticarte para subir archivos

Si ya puedes subir cambios a GitHub desde Git, continúa con el apartado 3.
Si todavía no tienes configurada la autenticación, una opción guiada es instalar
[GitHub CLI](https://cli.github.com/) y ejecutar:

```bash
gh auth login
```

Elige **GitHub.com**, **HTTPS**, autenticar Git con tu cuenta si lo pregunta y
**Login with a web browser**. Sigue las instrucciones del navegador. GitHub CLI
configura las credenciales que utilizará Git al subir tu trabajo.
Git Credential Manager es otra opción compatible si ya lo tienes configurado.
[Referencia: autenticación para Git por HTTPS](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git).

## 3. Crear tu repositorio personal en GitHub

1. Inicia sesión en GitHub y selecciona **New repository**.
2. Como propietario, selecciona tu cuenta personal.
3. Ponle un nombre, por ejemplo `sii-26-27`.
4. Selecciona **Private**.
5. Déjalo **vacío**: no añadas README, `.gitignore` ni licencia en este paso.
6. Pulsa **Create repository** y conserva su dirección HTTPS. Será parecida a
   `https://github.com/TU_USUARIO/sii-26-27.git`.

No pulses **Fork** ni crees el repositorio desde una plantilla. Partiremos del
historial del profesor mediante un clon y lo subiremos a este repositorio vacío.
Si utilizas otro nombre, cambia `sii-26-27` en las direcciones de los comandos.

## 4. Clonar los materiales y conectar tu repositorio

Este apartado se hace **una sola vez**. Sitúa la terminal en la carpeta donde quieras
guardar el curso. El comando creará una carpeta nueva llamada `SII`.

Si ya tienes una carpeta `SII` con trabajo anterior, elige otra ubicación para este
clon y conserva la carpeta anterior hasta haber incorporado tus ejercicios.

Sustituye `TU_USUARIO` en la dirección de tu repositorio y ejecuta:

```bash
git clone --branch main --origin upstream https://github.com/MAIIND/sistemas-industriales-inteligentes-26-27-estuds.git SII
cd SII
git remote add origin https://github.com/TU_USUARIO/sii-26-27.git
```

`--origin upstream` pone el nombre `upstream` al repositorio del profesor. Después
añadimos el tuyo con el nombre `origin`. Conserva la carpeta oculta `.git`, que
contiene el historial y esta configuración.
[Referencia: remotos en Git](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes).

Dentro de `SII`, configura el funcionamiento de `pull` y `push`:

```bash
git config --local remote.pushDefault origin
git config --local push.default current
git config --local branch.main.rebase false
git config --local pull.ff true
git config --local branch.main.mergeOptions "--no-edit"
```

Estas opciones se guardan únicamente en este clon. Las dos primeras envían las
subidas a tu repositorio. Las restantes incorporan las novedades del profesor
mediante una fusión y utilizan el mensaje de fusión predeterminado, sin abrir un editor.

Sube la copia inicial:

```bash
git push origin main
```

Utiliza el comando tal como aparece, **sin añadir `-u`**, para conservar `upstream/main`
como referencia de descarga. Entra en tu repositorio en el navegador y comprueba
que aparecen los materiales.

### Comprobar los dos destinos

```bash
git remote -v
git branch -vv
git config --get remote.pushDefault
git status
```

Comprueba que `upstream` tiene la dirección del profesor y `origin` la tuya. La rama
`main` debe mostrar `[upstream/main]`, posiblemente acompañado de información sobre
commits adelantados o atrasados. La consulta `remote.pushDefault` debe responder
`origin`. Tu trabajo puede aparecer adelantado respecto a `upstream/main`: es
normal, porque incluye tus respuestas.

## 5. Dar acceso al profesor

Aunque le envíes el enlace, el profesor necesita una invitación para abrir tu
repositorio privado:

1. Abre **tu repositorio** en GitHub.
2. Entra en **Settings → Collaborators**, dentro de la sección **Access**.
3. Pulsa **Add people**.
4. Introduce el correo de GitHub del profesor: **`amlopez@uniovi.es`**.
5. Comprueba que es la persona correcta y envía la invitación.
6. Comunícale la dirección de tu repositorio por el canal indicado en el Campus.
7. Verifica después que la invitación ha sido aceptada y ya aparece como colaborador.

Invítalo **como colaborador del repositorio**; no compartas tu contraseña ni tus
credenciales. En los repositorios personales, el rol de colaborador permite también
contribuir a los archivos; el profesor lo utilizará para la revisión acordada.
[Referencia: invitar colaboradores](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository).

## 6. Preparar Python y los datos

Abre **la carpeta `SII` completa** en VS Code. Sigue la
[guía del entorno Python](entorno_python_vscode_guia.md) para preparar `.venv` y
seleccionar el kernel. Con este procedimiento, la carpeta y los materiales ya se
obtienen mediante el clon.

Descarga los datasets que indique el profesor y conserva la estructura:

```text
SII/
├── .git/
├── .venv/
├── docs/
│   └── requirements.txt
├── datasets/
│   └── dataset_flotacion_mini.csv
└── semana-01/
    └── Semana1_ALUMNO.ipynb
```

Los cuadernos buscan los datos desde la carpeta de su semana, mediante rutas como
`../datasets/`. Mantén esa estructura al ejecutar. Los datos grandes se descargan
aparte según las instrucciones del curso.

## 7. Guardar y subir tus ejercicios

Trabaja en el cuaderno base de la semana conservando su nombre. Guarda el archivo
en VS Code. Antes de entregar, comprueba su ejecución de principio a fin con el
kernel indicado y conserva las salidas que pida el enunciado.

Desde la raíz `SII`, por ejemplo para S1:

```bash
git status
git add semana-01/Semana1_ALUMNO.ipynb
git diff --cached --stat
git commit -m "Completar ejercicios guiados de S1"
git push
```

`git add` selecciona los archivos que vas a guardar; `git commit` registra esa versión
localmente; `git push` la envía a tu repositorio. Un commit por sí solo no sube nada.
Para otras semanas o versiones, sustituye la ruta por el archivo que hayas trabajado.
Añade también los archivos auxiliares necesarios que pida la tarea, seleccionándolos
por su ruta.

Revisa qué vas a subir. Mantén en tu ordenador `.venv`, los datos grandes y cualquier
archivo de credenciales, como `.env`. En estos ejemplos seleccionamos archivos
concretos; evita añadir toda la carpeta de golpe con `git add .`.

Después de `push`, abre tu repositorio y comprueba que aparecen el último commit y
el cuaderno actualizado. Mantén ese acceso durante la revisión del curso.

## 8. Recibir nuevas semanas y correcciones

Antes de actualizar, guarda tus cuadernos y registra tus cambios con los pasos del
apartado 7. Si `git status` muestra archivos modificados o pendientes de añadir,
revísalos antes de continuar.

Con el trabajo guardado en commits y sin una operación pendiente:

```bash
git pull
```

Este comando incorpora las novedades de `upstream/main` utilizando la configuración
del apartado 4. Una semana nueva se añadirá junto a las anteriores. Si todo termina
correctamente, guarda también la actualización en tu repositorio:

```bash
git push
```

Git intenta combinar el historial del profesor con el tuyo. Si ambos habéis cambiado
el mismo contenido, puede aparecer un conflicto; consulta el apartado 10.
[Referencia: incorporación de cambios con `git pull`](https://git-scm.com/docs/git-pull).

### Cuadernos corregidos con una nueva versión

Si el profesor publica, por ejemplo, `Semana1_ALUMNO_v2.ipynb` como archivo nuevo y
conserva el anterior, recibirás v2 al hacer `pull`. Tu cuaderno ya trabajado seguirá
en su sitio. Lee qué ha cambiado y sigue la indicación del profesor sobre aplicar
la corrección o trasladar tus respuestas a la nueva versión. Las respuestas no se
transfieren automáticamente entre archivos.

## 9. Identificar una entrega para su revisión

Sigue siempre el enunciado y el canal de entrega indicado. Si se solicita entrega
por enlace en el Campus Virtual:

1. Guarda tu trabajo, haz commit y comprueba que `git push` termina correctamente.
2. Abre el cuaderno en **tu repositorio de GitHub**.
3. Pulsa la tecla **Y** para obtener el enlace permanente a esa versión.
4. Copia ese enlace en la tarea del Campus e indica la versión base del cuaderno
   y los demás archivos que deban revisarse.

El enlace permanente incluye el identificador del commit en la dirección, en lugar
de `/main/`. Así el profesor puede revisar lo que entregaste aunque después sigas
trabajando. Comprueba antes que ha aceptado tu invitación.
[Referencia: enlaces permanentes](https://docs.github.com/en/repositories/working-with-files/using-files/getting-permanent-links-to-files).

La modalidad de entrega de cada tarea la fija el profesor. Esta guía no añade una
tarea evaluable ni una defensa oral a S1.

## 10. Problemas frecuentes

| Mensaje o situación | Qué comprobar |
|---|---|
| `git` no se reconoce | Instala Git y vuelve a abrir VS Code o la terminal. |
| `Repository not found` | Revisa usuario, URL y acceso. Sustituye los marcadores de ejemplo. |
| No existe la rama `main` | Confirma con el profesor la URL y la rama de materiales. |
| `Permission denied` o error de autenticación | Comprueba la cuenta con la que has iniciado sesión y la autenticación del apartado 2. |
| `nothing to commit` | Guarda el cuaderno en VS Code y comprueba `git status`; quizá ya estaba registrado. |
| `pull` pide guardar cambios locales | Registra tus archivos antes de repetir la actualización. |
| `push` rechazado porque hay cambios remotos | Revisa si has editado desde GitHub u otro ordenador; consulta el párrafo siguiente. |
| El profesor no puede abrir el enlace | Verifica que lo has invitado al repositorio correcto y que ha aceptado. |

Si trabajas desde otro equipo o editas desde la web, tu repositorio personal también
puede tener novedades. Con tus cambios locales guardados y sin conflictos pendientes,
recíbelas antes de subir:

```bash
git pull --no-rebase --no-edit origin main
git push
```

Ese `pull` explícito descarga de **tu repositorio**, mientras que el `git pull` habitual
descarga del profesor. Si aparece un conflicto, detente antes del `push`.

### Si aparece un conflicto

Git mostrará `CONFLICT` y `git status` identificará los archivos afectados. No
ejecutes ni guardes desde Jupyter un notebook con conflictos sin resolver. Para
volver al estado anterior a esta fusión, si comenzaste con tus cambios guardados:

```bash
git merge --abort
git status
```

Conserva tu trabajo y pide ayuda al profesor indicando el mensaje y el archivo.
Evita intentar resolverlo borrando la carpeta, descartando cambios o forzando subidas.

## 11. Recordatorio de uso diario

| Quiero… | Comando, desde `SII` |
|---|---|
| Ver qué ha cambiado | `git status` |
| Seleccionar un cuaderno | `git add semana-01/Semana1_ALUMNO.ipynb` |
| Guardar una versión local | `git commit -m "Descripción del avance"` |
| Subir mi trabajo | `git push` |
| Recibir materiales del profesor, con el trabajo guardado | `git pull` |
| Comprobar las direcciones | `git remote -v` |

Recuerda: **guarda el archivo, haz commit y después push** para que el profesor
pueda ver tus avances en GitHub.
