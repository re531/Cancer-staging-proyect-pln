# Cancer-staging-proyect-pln

El entorno de ejecución requiere las dependencias especificadas. Para instalarlas, utiliza el archivo `requirements.txt`:

pip install -r requirements.txt

Ejecución del Sistema
El flujo completo de entrenamiento e inferencia se gestiona a través del notebook de evaluación:

Entorno: Asegúrate de tener todas las dependencias instaladas.

Entrenamiento e Inferencia: Abre el archivo notebooks/Evaluacion.ipynb en Jupyter Notebook o JupyterLab.

Pipeline: Ejecuta las celdas de forma secuencial. El notebook:

Carga los datos crudos desde Datos/Original/.

Entrena la arquitectura CNN (sin preprocesamiento).

Realiza la inferencia sobre Datos/A_Predecir/tcga_simple_test_empty.csv.

Exporta el archivo resultante a Datos/Predicciones/tcga_simple_test_predicho.csv.

Estrategia: Enfoque de extremo a extremo sin limpieza de texto para preservar el contexto clínico.

Manejo de Desbalanceo: Se implementaron pesos de clase (class_weights) para compensar la menor representación de las clases minoritarias (T4), logrando un rendimiento robusto en todos los estadios.