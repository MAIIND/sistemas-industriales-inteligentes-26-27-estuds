# El proceso y los datos del curso
### Planta de flotación de mineral de hierro

Durante las 8 semanas vamos a trabajar **siempre con el mismo conjunto de datos**: registros reales de una planta industrial que separa hierro de su impureza principal, la sílice. Conviene que entiendas de dónde salen los números antes de tocarlos.

## ¿Qué hace la planta?

Del yacimiento sale mineral de hierro mezclado con **sílice** (cuarzo, SiO₂), que es lo que no queremos. El objetivo de la planta es **quitar la sílice** para que el producto final —el *concentrado*— tenga mucho hierro y poca sílice.

Para separarlos se usa un truco que se llama **flotación**: el mineral molido se mezcla con agua formando una papilla (la *pulpa*), y se hace burbujear aire a través de ella. Las partículas que se han vuelto "repelentes al agua" se pegan a las burbujas y **suben** formando una espuma; las demás se quedan abajo.

Lo curioso es que aquí se hace al revés de lo que uno pensaría: **flota la sílice** (la basura, que se retira por arriba) y el **hierro se queda abajo** como concentrado. Por eso se llama *flotación reversa*.

¿Cómo se decide qué flota? Con tres "mandos" que ajusta el operador:

- **Amina**: hace que la sílice se vuelva repelente al agua → la sílice flota.
- **Almidón**: mantiene el hierro "mojable" → el hierro no flota, se queda en el concentrado.
- **pH** (en torno a 10,5): necesario para que la amina haga su trabajo.

Producto bueno = mucho hierro, **poca sílice**. Y aquí está lo importante para nosotros: **la cantidad de sílice que se cuela en el concentrado es lo que queremos predecir.**

## ¿Qué contiene cada fila de datos?

Cada registro describe el estado de la planta en un instante. Las columnas se agrupan en cuatro familias:

**Cuándo**
- `date` — la fecha y hora de la medida.

**Cómo entra el mineral** (la calidad de lo que llega; no se controla, depende de la mina)
- `% Iron Feed`, `% Silica Feed`.

**Los mandos del operador** (lo que la planta ajusta para controlar el proceso)
- `Starch Flow` (almidón) y `Amina Flow` (amina).
- `Ore Pulp Flow`, `Ore Pulp pH`, `Ore Pulp Density`.
- `Flotation Column 01–07 Air Flow` — el aire inyectado en cada una de las 7 columnas.
- `Flotation Column 01–07 Level` — el nivel de espuma en cada columna.
- La planta tiene 7 columnas de flotación, pero el dataset no indica cómo están conectadas entre sí (en serie, en paralelo…). Solo el aire y el nivel se miden columna a columna; todo lo demás es una sola medida para toda la planta.

**Cómo sale el producto** (la calidad final, medida en laboratorio)
- `% Iron Concentrate` — hierro en el concentrado.
- `% Silica Concentrate` — sílice en el concentrado. **Esta es nuestra variable objetivo.**

## Un detalle clave: los datos no van todos al mismo ritmo

Esto es importante y lo usaremos a lo largo del curso:

- Las variables **de proceso** (caudales, pH, aire, nivel…) se registran **cada 20 segundos**. Son rápidas y baratas: las da la propia instrumentación de la planta.
- Las variables **de calidad** (% de hierro y sílice) vienen de **análisis de laboratorio** y solo se tienen **una vez por hora**. Son lentas y caras.

Como en una hora caben 180 medidas de 20 segundos (3600 / 20 = 180), verás que **180 filas seguidas comparten el mismo valor de laboratorio**. No es un error del dato: es así como está construido, y aprender a manejarlo bien es parte del curso.

*(Matiz que descubrirás tú mismo en la Semana 1: en una fracción pequeña de horas —cuando el laboratorio tardó más de una hora entre dos medidas reales— el valor no es exactamente constante dentro de la hora, sino una rampa interpolada entre dos medidas reales. No lo des por sentado sin comprobarlo.)*

## ¿Qué vamos a hacer con esto?

La idea que recorre todo el curso es construir un **"sensor virtual"**: como el resultado de laboratorio tarda una hora en llegar, queremos **estimar el % de sílice al momento** a partir de las variables rápidas de proceso. Así el operador podría corregir la marcha de la planta sin esperar al laboratorio.

En la **Semana 1** empezaremos por lo básico: cargar estos datos, entenderlos, y resumir las 180 medidas de cada hora en una tabla ordenada y manejable con la que trabajaremos después. No hace falta saber química ni tener experiencia previa con datos: iremos paso a paso.
