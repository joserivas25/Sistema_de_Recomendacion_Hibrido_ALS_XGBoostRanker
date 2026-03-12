# Sistema_de_Recomendacion_Hibrido_ALS_XGBoostRanker
Este proyecto implementa un motor de recomendación avanzado de dos etapas diseñado para manejar el problema de "Cold Start" y optimizar la relevancia de las sugerencias mediante un modelo de re-ranking. Combina la potencia del filtrado colaborativo con algoritmos de boosting para personalización a gran escala.


🏗️ Arquitectura del Sistema: Pipeline de Dos Etapas
El sistema sigue la arquitectura moderna de los motores de recomendación utilizados por empresas como Netflix o Pinterest, dividida en Generación de Candidatos y Ranking.

1. Etapa de Recuperación (Candidate Generation)
En esta fase, el objetivo es reducir millones de posibles productos a unos pocos cientos de candidatos relevantes para el usuario.

Algoritmo: ALS (Alternating Least Squares) implementado en PySpark.

Técnica: Filtrado Colaborativo Basado en Matrices Factorizadas. El modelo descompone la matriz de interacciones usuario-producto en vectores latentes (embeddings).

Función: Identifica patrones de comportamiento similares entre usuarios para predecir la afinidad hacia productos no interactuados.

Escalabilidad: Al ejecutarse sobre Spark, el entrenamiento de ALS se distribuye en múltiples nodos del clúster de Databricks.

2. Etapa de Ranking (Re-Ranking con XGBoost)
Una vez obtenidos los candidatos, se utiliza un modelo mucho más "pesado" y preciso para ordenar la lista final.

Algoritmo: XGBoost Ranker.

Metodología: A diferencia de una clasificación simple, se utiliza un enfoque de Learning to Rank (LTR).

Features (Características): El modelo no solo usa la puntuación del ALS, sino que integra metadatos adicionales:

Características del usuario (demografía, historial).

Características del producto (categoría, precio, tendencia).

Interacciones cruzadas.

Función: Refina el orden de los candidatos basándose en la probabilidad real de conversión o clic, optimizando métricas de negocio.

🛠️ Especificaciones Técnicas
Entorno: Databricks (Spark Runtime para ETL y entrenamiento distribuido).

Machine Learning:

pyspark.ml.recommendation.ALS para el filtrado colaborativo.

xgboost.XGBRanker para el modelo de clasificación de relevancia.

Procesamiento de Datos:

Uso de Spark SQL para la ingeniería de características (Feature Engineering).

Indexación de variables categóricas mediante StringIndexer.

Optimización: Implementación de pipelines de evaluación para medir el RMSE en la etapa de ALS y el nDCG (Normalized Discounted Cumulative Gain) en la etapa de ranking.

🚀 Flujo de Ejecución en el Notebook
Preparación de Datos: Carga de interacciones históricas y metadatos de clientes/productos.

Entrenamiento ALS: Generación de factores latentes y extracción de los top-K candidatos por usuario.

Feature Join: Cruce de los candidatos con características ricas (features) para alimentar al ranker.

Entrenamiento XGBoost: Ajuste del modelo de ranking para predecir la posición ideal de cada producto.

Inferencia: Generación de la lista final de recomendaciones personalizadas.

⚖️ Copyright y Propiedad Intelectual
© 2025 [joserivas25] - Todos los derechos reservados.

Aviso Legal
Este repositorio contiene una implementación técnica de un sistema de recomendación híbrido con fines de exhibición de portafolio profesional.

Restricciones: Queda estrictamente prohibida la reproducción, distribución o uso comercial de la arquitectura de datos y la lógica de integración ALS-XGBoost presentada en este proyecto sin autorización escrita.

Uso Autorizado: El código se publica para revisión técnica, auditoría de habilidades y fines educativos. No se otorga licencia para la implementación de este pipeline en entornos de producción de terceros.

Privacidad: Los datos utilizados en los ejemplos han sido anonimizados o son sintéticos para proteger la confidencialidad de la información de negocio.
