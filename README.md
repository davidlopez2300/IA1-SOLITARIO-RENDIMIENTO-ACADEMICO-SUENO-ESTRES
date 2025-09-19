

# Proyecto: Análisis y Predicción del Rendimiento Académico en Estudiantes Universitarios a partir de Patrones de Sueño y Estrés

### Identificación del proyecto

* **Curso:** Inteligencia Artificial I – 2025-2 C1
* **Equipo:** Solitario
* **Integrantes:**

  * Juan David Lopez Ruiz – Código UIS: 2180645
  

---

##  Descripción de los datos a usar

* **Dataset principal:** Stress and Sleep Patterns
* **Enlace:** https://data.mendeley.com/datasets/5mvrx4v62z/3
* **Cantidad de datos:** El conjunto de datos consta de 16 columnas en formatos categóricos u ordinales. Contiene mas de 900 filas sin datos faltantes, lo que lo prepara para aplicaciones de análisis y aprendizaje automático.
* **Posibles datasets complementarios:** Se evaluarán otras fuentes que incluyan variables adicionales como uso de pantallas antes de dormir o frecuencia de ejercicio.

---

##  Preguntas a responder

### Antes del EDA (conceptual)

**Problema y relevancia:**
El bajo rendimiento académico de los estudiantes universitarios está fuertemente asociado con factores de salud como la falta de sueño y altos niveles de estrés. Estos factores, tanto físicos (horas de sueño) como psicológicos (estrés percibido), impactan directamente en el bienestar y desempeño académico. Predecir el rendimiento a partir de estas variables permitiría anticipar riesgos y diseñar estrategias de apoyo para mejorar la vida estudiantil.

**Objetivo del análisis:**
La primera fase del análisis exploratorio (EDA) busca identificar patrones entre sueño, estrés y rendimiento académico. Esto permitirá definir las variables más relevantes, verificar la calidad de los datos y orientar la construcción de un modelo predictivo robusto que explique cómo influyen estos factores en las notas de los estudiantes.

**Métricas o indicadores:**
Se evaluarán correlaciones entre horas de sueño, estrés percibido y rendimiento académico. Además, se emplearán métricas de predicción como error cuadrático medio (RMSE) en regresión o accuracy/F1-score en clasificación. Estas métricas permiten medir la capacidad del modelo para predecir notas y, a su vez, cuantificar el impacto de los factores de sueño y estrés en el desempeño.

**Motivación de la elección:**
Se eligió este problema porque combina variables físicas y mentales claves para los universitarios. Además, tiene un impacto directo en la salud y el rendimiento, lo que lo hace relevante para la comunidad académica y para el desarrollo de soluciones prácticas.

---

### Después del EDA (basado en datos)

**Datos utilizados:**
Se usaron datos del dataset *Stress and Sleep Patterns*, compuesto principalmente por tablas numéricas y categóricas que describen hábitos de sueño, niveles de estrés y rendimiento académico.

**Información contenida en los datos:**
El dataset incluye variables relacionadas con la cantidad de horas de sueño, calidad percibida del descanso, nivel de estrés auto-reportado, actividad física, uso de dispositivos electrónicos y desempeño académico (notas). Estas características permiten estudiar el efecto combinado del sueño y el estrés en el rendimiento, y explorar la posible influencia de factores secundarios como el ejercicio o el uso de pantallas.

**Desafíos asociados a los datos:**
Se identifican posibles valores faltantes o inconsistentes en las variables auto-reportadas (estrés percibido, calidad del sueño). El tamaño relativamente pequeño del dataset limita la generalización de los resultados. Además, puede existir sesgo en la muestra, ya que se centra en un grupo específico de estudiantes y no necesariamente representa a toda la población universitaria. Otro desafío es el equilibrio de clases en el rendimiento académico, que podría afectar la precisión de los modelos predictivos.

---


