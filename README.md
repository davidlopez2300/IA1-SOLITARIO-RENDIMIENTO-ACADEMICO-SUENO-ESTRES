

# Proyecto: Análisis y Predicción de Rendimiento Académico: El Impacto de los Hábitos Diarios

### Identificación del proyecto

* **Curso:** Inteligencia Artificial I – 2025-2 C1
* **Equipo:** Solitario
* **Integrantes:**

  * Juan David Lopez Ruiz – Código UIS: 2180645
  

---

##  Descripción de los datos a usar


## Descripción de los Datos a Usar

**Dataset Principal:** `student_habits_performance.csv` (Derivado de fuentes académicas similares a "Stress and Sleep Patterns").

* **Variables Clave:** El conjunto de datos consta de **16 columnas** que incluyen variables cuantitativas (ej. `study_hours_per_day`, `sleep_hours`, `social_media_hours`) y variables categóricas u ordinales (ej. `diet_quality`, `part_time_job`).
* **Cantidad de Datos:** Contiene **1000 filas** sin datos faltantes, lo que lo prepara óptimamente para aplicaciones de análisis y Machine Learning.
* **Variable Objetivo (Transformada):** `Performance_Level` (Clasificación Multiclase: **Bajo (0), Medio (1), Alto (2)**).

---

## ❓ Preguntas a Responder

### Antes del EDA (Conceptual y Metodológico)

| Aspecto | Descripción Actualizada |
| :--- | :--- |
| **Problema y Relevancia** | El bajo rendimiento está ligado a una gestión ineficiente de factores del día a día (sueño, uso de pantallas, dieta). Predecir el rendimiento en tres niveles (Bajo, Medio, Alto) permite diseñar **estrategias de intervención focalizadas** para cada grupo, maximizando el apoyo estudiantil. |
| **Objetivo del Análisis** | **Fase 1 (EDA):** Identificar patrones de correlación entre hábitos diarios y el rendimiento. **Fase 2 (ML):** Construir un **Modelo de Clasificación Multiclase** (Random Forest) robusto para predecir si un estudiante caerá en el nivel Bajo, Medio o Alto, permitiendo la **intervención temprana**. |
| **Métricas o Indicadores** | Se emplean métricas de clasificación multiclase: **Accuracy** (Precisión General) y **Reporte de Clasificación (Precision, Recall, F1-score)** por clase. La optimización busca mejorar el F1-score en la clase **Medio (1)**, que es la más difícil de predecir. |
| **Motivación de la Elección** | Elegimos este enfoque porque provee una herramienta **accionable** para la comunidad académica. La clasificación multiclase es más útil que la binaria para la gestión de recursos y la orientación personalizada del estudiante. |

---

### Después del EDA y Modelado (Basado en Datos)

#### 1. Información Clave Contenida en los Datos (Hallazgos EDA)

El análisis exploratorio reveló las siguientes correlaciones con la variable objetivo `Performance_Level`:

* **Estudio y Rendimiento:** Existe una **fuerte correlación positiva**. La mediana de **`study_hours_per_day`** aumenta progresivamente del nivel Bajo al Alto.
* **Distracción Digital:** Hay una **clara correlación negativa** con el uso de redes sociales (`social_media_hours`). Los estudiantes de bajo rendimiento tienen consistentemente las medianas de uso de redes sociales más altas.
* **Bienestar:** La calidad del sueño (`sleep_hours`) y la calidad de la dieta (`diet_quality`) se correlacionan positivamente con el rendimiento Alto. La participación extracurricular también está más equilibrada en los grupos Medio y Alto, sugiriendo una buena gestión del tiempo.

#### 2. Desafíos Asociados a los Datos y al Modelado

* **Clasificación Media (Clase 1):** El principal desafío del modelo multiclase es la predicción del nivel **Medio (1)**. Esta clase tiene una menor Precisión (`Precision` < 0.70 en el modelo base) debido a que sus patrones de hábitos se superponen con los límites de las clases Bajo y Alto.
* **Sesgo en Variables Auto-Reportadas:** La precisión de variables como `mental_health_rating` o `diet_quality` depende del reporte honesto del estudiante, lo que puede introducir ruido o sesgo.

#### 3. Metodología de Machine Learning y Resultados

* **Modelo Elegido:** **Random Forest Classifier (Clasificación Multiclase)**.
    * **Justificación:** El Random Forest es robusto, maneja bien datos mixtos (categóricos y numéricos), y proporciona la **importancia de las características** para justificar las intervenciones.
* **Optimización:** Se aplicó **Grid Search** para afinar hiperparámetros (`n_estimators`, `max_depth`, etc.) y mejorar el rendimiento.
* **Métrica de Éxito:** El modelo fue optimizado para maximizar el `Accuracy` general y el `F1-score` de la clase **Medio (1)**.

| Modelo | Precisión Base (Accuracy) | Precisión Optimizada (Accuracy) |
| :--- | :--- | :--- |
| **Random Forest** | 0.7867 | *[Aquí se pondrá el resultado final de tu Grid Search]* |

* **Próximo Paso:** Una vez ejecutada la optimización, se actualizará el campo de Precisión Optimizada y se analizarán las variables de **Feature Importance** para comunicar a la comunidad académica cuáles son los hábitos con mayor impacto predictivo.
---


