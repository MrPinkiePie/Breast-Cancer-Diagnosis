# 🎗️ Breast Cancer Diagnosis: Support Vector Machines (SVM)

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange?style=flat&logo=scikit-learn)
![Model](https://img.shields.io/badge/Model-SVM-green)
![Status](https://img.shields.io/badge/Status-Completado-success)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1fYctXU9222vshA7wbC2ZnKZxDx6e3ROh?usp=sharing)

## 📋 Descripción del Proyecto
Este proyecto aplica algoritmos de **Support Vector Machines (SVM)** para asistir en el diagnóstico médico de cáncer de mama. Utilizando el dataset *Wisconsin Diagnostic Breast Cancer (WDBC)*, el objetivo no es solo la exactitud técnica, sino la **seguridad clínica**: priorizar la detección de todos los casos malignos (Recall) para salvar vidas.

Este trabajo marca una transición en mi portafolio, pasando de modelos basados en árboles (XGBoost/Random Forest) a modelos basados en geometría y márgenes, ideales para datasets de alta dimensionalidad.

## 🏥 Contexto y Problemática
En el diagnóstico oncológico, los errores de predicción tienen costos asimétricos extremos:
* **Falso Positivo (Error Tipo I):** Diagnosticar a un paciente sano como enfermo. Conlleva costos económicos y ansiedad, pero no es letal.
* **Falso Negativo (Error Tipo II):** Diagnosticar a un paciente con cáncer como sano. **Este error es inaceptable**, ya que retrasa el tratamiento.

**Objetivo:** Desarrollar un clasificador binario que maximice el **Recall (Sensibilidad)**, minimizando los Falsos Negativos.

## ⚙️ Estrategia de Modelado
Se eligió SVM con kernel **RBF** por su robustez en espacios de alta dimensionalidad (30 features).

### Decisiones Técnicas Clave:
1.  **Estandarización Rigurosa (`StandardScaler`):** SVM se basa en distancias euclidianas. Variables de gran magnitud (ej. Área ~1000) dominarían sobre las pequeñas (ej. Simetría ~0.1). Se escalaron todas las características.
2.  **Manejo del Desbalance (`class_weight='balanced'`):** Se penalizó el error en la clase minoritaria (Maligno) para forzar al modelo a prestarle atención.
3.  **Regularización Conservadora (`C=0.1`):** Se optó por un margen "suave" (Soft Margin). Esto crea un modelo más generalista que prefiere tolerar algunos errores en el entrenamiento a cambio de no sobreajustarse al ruido (evitando Overfitting).
4.  **Optimización:** `GridSearchCV` optimizando específicamente la métrica `Recall`.

## 📂 Sobre el Dataset
**Fuente:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+%28Diagnostic%29)
* **Instancias:** 569 pacientes.
* **Target:** Diagnosis (M = Malignant, B = Benign).
* **Features:** 30 características geométricas computadas a partir de imágenes digitalizadas de aspirados con aguja fina (FNA).

## 🛠️ Stack Tecnológico
* **Procesamiento:** Pandas, NumPy.
* **Visualización:** Seaborn, Matplotlib.
* **Preprocesamiento:** `StandardScaler`.
* **Modelado:** `SVC` (Scikit-Learn).
* **Interpretación:** `permutation_importance`, `PCA`.

## 📈 Resultados del Modelo
El modelo final logró un equilibrio robusto para un entorno de asistencia médica:

| Métrica | Valor | Interpretación |
| :--- | :--- | :--- |
| **Recall (Sensibilidad)** | **~95%** | El modelo detecta casi la totalidad de los casos de cáncer. |
| **ROC - AUC** | **0.99** | Excelente capacidad de separación entre clases sanas y enfermas. |
| **Accuracy** | **~87%** | Ligeramente menor debido al trade-off: se aceptan más Falsos Positivos (baja precisión) para asegurar el alto Recall. |

**Mejores Hiperparámetros:**
* `C`: 0.1
* `gamma`: 0.1
* `kernel`: 'rbf'

## 🔍 Insights: ¿Qué define a un tumor maligno?
Mediante **Permutation Importance** y **PCA**, auditamos la "caja negra" del modelo:

### 1. Importancia de Variables
Al analizar qué variables impactan más en el diagnóstico, descubrimos:
* **El peligro de lo "Peor" (`_worst`):** Las variables más predictivas fueron `radius_worst`, `perimeter_worst` y `area_worst`. El modelo busca las células más grandes y anómalas de la muestra, no el promedio.
* **La forma importa:** La irregularidad del contorno (`concave_points`) es crítica. Los tumores malignos tienen bordes espiculados.
* **Ruido:** Variables como *Textura* o *Simetría* resultaron menos determinantes que la geometría física.

### 2. Visualización 2D (PCA)
Se redujeron las 30 dimensiones a 2 Componentes Principales que explican el **~63% de la varianza**.
* **Conclusión Visual:** Existe una separación geométrica clara entre los clusters de Benignos y Malignos, lo que justifica matemáticamente el alto rendimiento del SVM (AUC 0.99).

---
*Este proyecto fue desarrollado como parte de un portafolio de Data Science enfocado en la diversificación de algoritmos de Machine Learning.*
