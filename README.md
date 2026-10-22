*Redes Neuronales Feed-Forward (MLP): Clasificación y Regresión*

Proyecto de bonificación sobre Redes Neuronales Artificiales con el perceptrón multicapa (MLP) usando Keras / TensorFlow. Se resuelven dos problemas con datasets del UCI Machine Learning Repository:

Clasificación multiclase: estado fetal (Normal / Sospechoso / Patológico) a partir de cardiotocogramas.
Regresión: predicción de la humedad absoluta (AH) a partir de sensores de calidad del aire.

Autor: Jaime Alberto Castro Tamayo - Joseph García Llano Institución: Universidad de Medellín, Facultad de Ingenierías

Contenido
Datasets
Metodología
Arquitecturas
Resultados
Estructura del repositorio
Instalación y ejecución
Limitaciones y mejoras futuras
Referencias
Datasets
Problema	Dataset	Registros	Variable objetivo
Clasificación	Cardiotocography	2126	NSP (1 = Normal, 2 = Sospechoso, 3 = Patológico)
Regresión	Air Quality	9357 (horarios)	AH (humedad absoluta, escalada x10)

El dataset de Air Quality se descarga automáticamente al ejecutar el notebook (requiere conexión a internet). El de cardiotocografía debe estar en la misma carpeta con el nombre DB_Fetal_Cardiotocograms.txt.

Metodología
Preprocesamiento
Clasificación: codificación One-Hot de la variable de salida.
Regresión: los valores -200 marcan datos perdidos. Se eliminan los registros sin variable de salida y se imputan las características faltantes con la media de la columna.
Validación cruzada de 10 folds (KFold) para estimar el desempeño como promedio ± desviación estándar.
Experimentación de hiperparámetros: se varía el número de épocas y de neuronas en las capas ocultas, y se registran la eficiencia (o el error) y el tiempo de ejecución.
Visualización: gráfica de salidas reales vs. predicciones de la red para la mejor configuración.
Arquitecturas
	Clasificación	Regresión
Capas ocultas	Dense(10, ReLU) y opcionalmente Dense(2, ReLU)	Dense(10 o 20, ReLU)
Capa de salida	Dense(3, Softmax)	Dense(1, Lineal)
Función de pérdida	Entropía cruzada categórica	Error absoluto medio (se reporta ECM)
Optimizador	Adam	Adam
Tamaño de lote	32	100
Métrica reportada	Accuracy	Error cuadrático medio (ECM)
Resultados

La columna "±" corresponde a la desviación estándar entre los 10 folds.

Clasificación (Cardiotocografía)
Épocas	Neuronas capa 1	Neuronas capa 2	Eficiencia ± desv.	Tiempo (s)
10	10	N/A	0.897 ± 0.055	37.2
30	10	N/A	0.929 ± 0.028	71.7
10	10	2	0.778 ± 0.039	54.6
30	10	2	0.867 ± 0.036	79.0
50	10	2	0.778 ± 0.039	121.7
Regresión (Air Quality)
Épocas	Neuronas	ECM ± desv.	Tiempo (s)
10	10	246.11 ± 164.29	53.4
10	20	115.49 ± 97.12	53.5
100	10	68.69 ± 83.12	305.8
Estructura del repositorio
.
├── Proyecto_Sobre_RNA_Bonificacion_ML.ipynb   # Notebook principal
├── DB_Fetal_Cardiotocograms.txt               # Dataset de cardiotocografía
├── requirements.txt                           # Dependencias
├── .gitignore
├── LICENSE
└── README.md
