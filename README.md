# Cancer-staging-proyect-pln
# Manual de Ejecución del Sistema Final

Este documento explica los pasos necesarios para reproducir el entrenamiento del modelo final y generar las predicciones sobre el conjunto de test.

## 1. Requisitos del Entorno
Para evaluar el sistema, se han exportado todas las dependencias exactas del proyecto. Se recomienda crear un entorno virtual de Python (versión 3.9 o superior) y ejecutar el siguiente comando en la terminal para instalar las librerías necesarias:

``` bash

pip install -r requirements.txt

```


## 2. Estructura de Directorios Esperada
El código de evaluación (`Evaluacion.ipynb`) utiliza rutas relativas para localizar los datos. Para que la ejecución sea correcta, la estructura de carpetas del proyecto debe ser la siguiente:

```text
/Directorio_Raiz
 ├── /Datos
 │    ├── /Original
 │    │    └── tcga_simple_train.csv      <-- Datos de entrenamiento empleados por las diferentes decisiones tomadas
 |    |                                       ya que empelamos el texto "crudo" por ser el que mejor resultado nos ha dado a lo largo del proyecto
 |    |---/Preprocesados
 |    |     |---- tcga_preprocesado.csv   <-- Datos preprocesados guardados para poder ir haciendo las consecuentes pruebas de forma mas rapida
 |    |                                       y mas comoda.
 │    └── /A_Predecir
 │         └── tcga_simple_test_empty.csv <-- Datos de test sin etiquetas
 ├── /Notebooks 
 │    └── Evaluacion.ipynb                <-- Script principal de ejecución

 3. Instrucciones de Ejecución
Para obtener las predicciones finales, sigue estos pasos:

Ubicación del código: Abre el archivo Evaluacion.ipynb utilizando Jupyter Notebook, Jupyter Lab o tu IDE de preferencia.

Verificación de archivos: Asegúrate de que los archivos .csv mencionados en la estructura de directorios están en sus rutas correspondientes. El notebook leerá automáticamente los datos de entrenamiento limpios (tcga_preprocesado.csv) y el dataset vacío para test (tcga_simple_test_empty.csv).

Ejecución del pipeline: Ejecuta todas las celdas del notebook. El proceso realizará de forma desatendida las siguientes acciones:

Codificación de las etiquetas con LabelEncoder.

Tokenización y padding de los textos (longitud 300, vocabulario 5000).

Cálculo de pesos balanceados (class_weight) para contrarrestar el desbalanceo de clases (especialmente para la detección crítica del estadio T4).

Entrenamiento de una Red Neuronal Convolucional 1D (CNN) durante 10 épocas.

Inferencia sobre los datos del conjunto de test.

Obtención de Resultados: Una vez finalizada la ejecución, el script rellenará un archivo ,cogiendo las columnas del original de test añadiendo la columna t con las predicciones. Encontrarás tus resultados en:
../Datos/A_Predecir/tcga_simple_test_predicted.csv

4. Breve descripción de la Arquitectura
El modelo implementado es una arquitectura profunda secuencial compuesta por:

Una capa de Embedding para la representación semántica densa de las secuencias.

Una capa convolucional unidimensional (Conv1D) para la extracción de características locales del texto, seguida de GlobalMaxPooling1D.

Una red densa completamente conectada con fuerte regularización Dropout (0.75) para evitar el sobreajuste.

Una capa de salida con activación softmax para la clasificación probabilística multiclase de los estadios tumorales.
