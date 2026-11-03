DATOS DEL CURSO — Sistemas Industriales Inteligentes
===================================================

Todos los datos se descargan de la carpeta de datos del curso:
https://drive.google.com/drive/folders/1UVhDdCW6bLvXU8L0BaK7CulrtUaVzeT-?usp=sharing

Guarda cada fichero en esta carpeta, conservando exactamente su nombre:
  SII/datasets/<nombre del fichero>

Los cuadernos se ejecutan desde la carpeta de su semana (SII/semana-0N/) y buscan
los datos en ../datasets/. Descarga solo lo que pida cada semana.


SEMANA 1 · dato real
--------------------
  dataset_flotacion_mini.csv
      Recorte crudo: 20.000 filas y 24 columnas, con 112 horas. Procede de
      Quality Prediction in a Mining Process, de edumagalhaes:
      https://www.kaggle.com/datasets/edumagalhaes/quality-prediction-in-a-mining-process
      La práctica construye flotacion_horaria_mini.csv (112 filas y 13 columnas).
      Conserva ese resultado local junto al cuaderno ejecutado.


SEMANAS 2 A 8 · proyecto ancla (dato semisintético)
---------------------------------------------------
Desde la Semana 2 el proyecto ancla usa una versión semisintética del mismo
dataset: las variables de proceso son las reales (mismas horas y valores), y la
sílice del concentrado (con ella fuera_spec y el hierro del concentrado) se ha
simulado con un modelo del proceso que no se publica. Lo explica
docs/descripcion_dataset_flotacion.md.

  flotacion_semisintetica_horaria.csv              (Semanas 2 a 8)
      Tabla horaria: 4.097 horas y 13 columnas.
  flotacion_semisintetica_horaria_enriquecida.csv  (Semanas 2 a 8, ampliaciones)
      La misma tabla con el aire y el nivel de cada columna de flotación y las
      desviaciones típicas horarias: 34 columnas.
  flotacion_semisintetica_20s.csv                  (Semana 5)
      Registro completo a 20 s (~180 MB): 737.453 filas y 24 columnas, con el
      mismo formato que el crudo de Kaggle.


OTROS DATOS (ejercicios satélite)
---------------------------------
  Semana 3   ejemplos.csv, winequality-white.csv, winequality-red.csv,
             simpleclass_dataset.txt
  Semana 4   simpleclass_dataset.txt
  Semana 5   ejemplos.txt, DigitDataset/, flowers/ e images_alexnet/ (carpetas
             completas); ex4data1.csv es opcional


Esta carpeta está excluida de las subidas de trabajo, salvo este README; sigue el
enunciado si una entrega concreta pide adjuntar algún CSV al Campus Virtual.

Las licencias de los datos son independientes de la del material docente.
Consulta docs/descripcion_dataset_flotacion.md para conocer su significado.
