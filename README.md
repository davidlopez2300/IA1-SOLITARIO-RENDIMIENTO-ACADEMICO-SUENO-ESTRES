

# Proyecto: Análisis y Predicción de Rendimiento Académico: El Impacto de los Hábitos Diarios

### Identificación del proyecto

* **Curso:** Inteligencia Artificial I – 2025-2 C1
* **Equipo:** Solitario
* **Integrantes:**

  * Juan David Lopez Ruiz – Código UIS: 2180645
  

---

## Descripción de los Datos a Usar

**Dataset Principal:** `student_habits_performance.csv`(https://www.kaggle.com/datasets/jayaantanaath/student-habits-vs-academic-performance?resource=download)


**Video:**`Proyecto: Análisis y Predicción de Rendimiento Académico`(https://youtu.be/0MBABNBxmKU)

* **Variables Clave:** El conjunto de datos consta de **16 columnas** que incluyen variables cuantitativas (ej. `study_hours_per_day`, `sleep_hours`, `social_media_hours`) y variables categóricas u ordinales (ej. `diet_quality`, `part_time_job`).
* **Cantidad de Datos:** Contiene **1000 filas** sin datos faltantes, lo que lo prepara óptimamente para aplicaciones de análisis y Machine Learning.
* **Variable Objetivo (Transformada):** `Performance_Level` (Clasificación Multiclase: **Bajo (0), Medio (1), Alto (2)**).

---

## Preguntas a Responder

### Antes del EDA (Conceptual y Metodológico)

| Aspecto | Descripción Actualizada |
| :--- | :--- |
| **Problema y Relevancia** | El bajo rendimiento está ligado a una gestión ineficiente de factores del día a día (sueño, uso de pantallas, dieta). Predecir el rendimiento en tres niveles (Bajo, Medio, Alto) permite diseñar **estrategias de intervención focalizadas** para cada grupo, maximizando el apoyo estudiantil. |
| **Objetivo del Análisis** | **Fase 1 (EDA):** Identificar patrones de correlación entre hábitos diarios y el rendimiento. **Fase 2 (ML):** Construir un **Modelo de Clasificación Multiclase** (Random Forest) robusto para predecir si un estudiante caerá en el nivel Bajo, Medio o Alto, permitiendo la **intervención temprana**. |
| **Métricas o Indicadores** | Se emplean métricas de clasificación multiclase: **Accuracy** (Precisión General) y **Reporte de Clasificación (Precision, Recall, F1-score)** por clase. La optimización busca mejorar el F1-score en la clase **Medio (1)**, que es la más difícil de predecir. |
| **Motivación de la Elección** | Elegimos este enfoque porque provee una herramienta **accionable** para la comunidad académica. La clasificación multiclase es más útil que la binaria para la gestión de recursos y la orientación personalizada del estudiante. |

---

# Metodológica del Proyecto: Predicción del Rendimiento Académico

Este documento resume las fases clave y las decisiones metodológicas tomadas en el desarrollo del modelo de Machine Learning para predecir el rendimiento académico (Bajo, Medio, Alto) a partir de los hábitos diarios del estudiante.

---

### I.  Definición del Problema y Preparación de Datos

Se optó por un enfoque de **Clasificación Multiclase** por su **utilidad práctica** para la intervención académica, siendo más valioso conocer la categoría de riesgo (Bajo/Medio/Alto) que un puntaje exacto.

1.  **Variable Objetivo:** La variable continua `exam_score` se transformó en `performance_level` (0, 1, 2) usando los **percentiles 33% y 66%** para asegurar un balance equitativo de clases.
2.  **Calidad de Datos:** Se confirmó la ausencia total de valores nulos y se procedió a la eliminación del identificador `student_id`.
3.  **Preprocesamiento:** Se aplicó **One-Hot Encoding (OHE)** a todas las variables categóricas. Los datos fueron divididos en conjuntos de Entrenamiento y Prueba (70/30) utilizando `stratify=y` para mantener el balance de clases en ambos subconjuntos.

---

### II.  Análisis Exploratorio de Datos (EDA)

El análisis visual confirmó las hipótesis iniciales sobre la relación entre hábitos y rendimiento:

* **Impacto Positivo:** El **Heatmap** y los diagramas de caja confirmaron que **`study_hours_per_day`** y **`attendance_percentage`** son los predictores positivos más fuertes.
* **Factores de Riesgo:** El **Diagrama de Dispersión** demostró que los estudiantes de rendimiento **Bajo (0)** se agrupan consistentemente en áreas de **Bajas Horas de Estudio y Altas Horas de Redes Sociales**.
* **Zona de Error:** La clase **Medio (1)** se localiza en la zona central de superposición, siendo el principal desafío para la clasificación.

---

### III.  Modelado y Optimización

Se eligió el **Random Forest Classifier** por su robustez ante datos mixtos y su capacidad de interpretar la importancia de las características.

#### A. Flujo de Modelado

| Paso | Propósito |
| :--- | :--- |
| **Modelo Base** | Entrenado con parámetros por defecto (`n_estimators=100`) para establecer un rendimiento inicial (Accuracy inicial **~0.7867**). |
| **Optimización** | Se implementó **Grid Search (`GridSearchCV`)** para realizar una búsqueda exhaustiva de la mejor combinación de hiperparámetros (`max_depth`, `n_estimators`, etc.) y maximizar el rendimiento general y el F1-score de la clase **Medio (1)**. |
| **Validación** | El modelo optimizado fue sometido a análisis de **Matriz de Confusión** y **Curvas ROC/AUC** para medir su capacidad discriminatoria y diagnosticar fallos en la predicción de la clase **Medio (1)**. |

#### B. Interpretación de Resultados

* **Matriz de Confusión:** Reveló que el error más frecuente es clasificar erróneamente a estudiantes **Medios (1)** como **Bajos (0)**, lo cual es crítico pero esperable dada la ambigüedad de la zona central.
* **Importancia de Variables:** Los principales impulsores predictivos del modelo son:
    1.  **`study_hours_per_day`** (Mayor influencia).
    2.  **`social_media_hours`** (Impacto negativo).
    3.  **`sleep_hours`** (Factor clave de bienestar).

Esta metodología asegura que el modelo no solo sea preciso, sino también **interpretable**, ofreciendo justificación clara para las estrategias de intervención académica.

---

## IV. Aprendizaje No Supervisado: Descubrimiento de Patrones Latentes

Una vez construidos y evaluados los modelos supervisados de predicción del rendimiento académico, se desarrolló una fase complementaria de **Aprendizaje No Supervisado**, cuyo objetivo fue identificar **patrones naturales** en los estudiantes sin utilizar etiquetas. Esta fase no pretende predecir rendimiento, sino **descubrir perfiles** que permitan entender mejor cómo se agrupan los estudiantes según sus hábitos, sueño y bienestar general.

### 1. Propósito del Análisis No Supervisado

El objetivo principal fue determinar si las variables de hábitos diarios y bienestar son capaces de formar **clusters coherentes**, es decir, grupos de estudiantes con características similares que puedan relacionarse indirectamente con los niveles de rendimiento académico observados.

Específicamente, se buscó:

- Identificar perfiles estudiantiles sin utilizar la variable objetivo.
- Analizar si hábitos de estudio, sueño y factores mentales generan separaciones naturales.
- Comparar diferentes algoritmos de clustering para evaluar estabilidad y calidad de los grupos.
- Visualizar estos patrones utilizando reducción de dimensionalidad.

---

## 2. Preprocesamiento y Selección de Características

Para esta fase, se trabajó únicamente sobre **variables numéricas**, ya que los algoritmos de clustering requieren espacios vectoriales formales.  
Los pasos aplicados fueron:

1. Eliminación de `student_id` y otras columnas irrelevantes.  
2. Selección de características numéricas del dataset.  
3. **Estandarización con `StandardScaler`** para ubicar todas las variables en la misma escala y evitar sesgos por magnitud.  
4. Preparación de una matriz final (`X_scaled`) utilizada por todos los algoritmos.

---

## 3. Algoritmos de Clustering Utilizados

Se implementaron tres de los métodos de agrupamiento más utilizados y complementarios entre sí:

### 🔹 **3.1 K-Means Clustering**

- Se utilizó el **Método del Codo (Elbow Method)** para estimar el número óptimo de clusters.
- El modelo fue entrenado con el valor de k más adecuado según la forma de curva de inercia.
- Se calculó el **Silhouette Score**, que mide la cohesión y separación entre grupos.

Este enfoque permite descubrir agrupaciones compactas y bien definidas.

---

### 🔹 **3.2 DBSCAN**

- Se aplicó `DBSCAN(eps=1, min_samples=5)`.
- Identifica grupos basados en densidad, permitiendo detectar:
  -En la practica del ejercicio detecto mayormente ruido.

Es especialmente útil porque no requiere especificar el número de clusters y detecta ruido naturalmente.

---

### 🔹 **3.3 Agglomerative Clustering (Jerárquico)**

- Permite modelar la estructura jerárquica de los datos y comparar cómo se agrupan los estudiantes desde niveles generales hasta segmentos específicos.

Este método complementa a K-Means y DBSCAN al analizar cómo los grupos pueden formarse de manera ascendente a partir de pares de observaciones.

---

## 4. Evaluación de la Calidad del Clustering

Para cada modelo se utilizó:

- **Silhouette Score**, que indica qué tan bien separados están los clusters.  
- Comparación entre métodos para evaluar consistencia de patrones.  

Gracias a estas métricas se verificó que los grupos formados no eran aleatorios y reflejaban diferencias reales en hábitos diarios.

---

## 5. Reducción de Dimensionalidad para Visualización

Dado que el dataset contiene múltiples variables, se aplicaron técnicas para proyectar los datos en 2 dimensiones y facilitar la interpretación visual.

### 🔸 **PCA – Análisis de Componentes Principales**

- Reduce la dimensionalidad preservando la mayor parte de la varianza.
- Permite visualizar los clusters de manera lineal.


### 🔸 **t-SNE – Proyección No Lineal**

- Proyecta datos en 2D preservando relaciones locales.
- Muestra agrupamientos complejos que no son visibles con PCA.









