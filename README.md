# 🎗️ Breast Cancer Diagnosis: Support Vector Machines (SVM)

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange?style=flat&logo=scikit-learn)
![Model](https://img.shields.io/badge/Model-SVM-green)
![Status](https://img.shields.io/badge/Status-En_Desarrollo-yellow)

## 📋 Descripción del Proyecto
Este proyecto aplica algoritmos de **Support Vector Machines (SVM)** para asistir en el diagnóstico médico de cáncer de mama. Utilizando características extraídas de imágenes digitalizadas de aspirados con aguja fina (FNA) de masas mamarias, el objetivo es clasificar los tumores como **Malignos (M)** o **Benignos (B)** con la mayor sensibilidad posible.

El proyecto marca un hito en mi portafolio al transicionar de modelos basados en árboles (XGBoost/Random Forest) a modelos basados en geometría y márgenes, ideales para datasets de alta dimensionalidad.

## 🎯 Objetivo
Desarrollar un clasificador binario que maximice el **Recall (Sensibilidad)**.
* **Contexto:** En medicina, un Falso Negativo (predecir "Benigno" cuando es cáncer) es fatal. Por tanto, optimizamos el modelo para minimizar estos errores, incluso si eso implica sacrificar ligeramente la precisión global.

## 🧠 ¿Por qué SVM (Support Vector Machines)?
A diferencia de proyectos anteriores, elegí SVM por sus ventajas matemáticas específicas para este problema:
1.  **Alta Dimensionalidad:** El dataset tiene 30 features numéricas. SVM es robusto en espacios de muchas dimensiones.
2.  **Márgenes Claros:** SVM busca el hiperplano que maximiza la distancia entre clases, lo que suele generalizar mejor en datos médicos con separaciones geométricas claras.
3.  **Kernels:** Permite proyectar los datos a dimensiones superiores para encontrar separabilidad lineal (Kernel Trick).

## 📂 Sobre el Dataset
**Fuente:** [UCI Machine Learning Repository - Breast Cancer Wisconsin (Diagnostic)](https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+%28Diagnostic%29)
* **Instancias:** 569 pacientes.
* **Target:** Diagnosis (M = Malignant, B = Benign).
* **Features:** 30 características reales computadas a partir de las imágenes (Radio, Textura, Perímetro, Área, Suavidad, etc.), calculadas en sus valores medios, error estándar y "peor" caso.

## 🛠️ Stack Tecnológico
* **Procesamiento:** Pandas, NumPy.
* **Visualización:** Seaborn, Matplotlib.
* **Preprocesamiento:** `StandardScaler` (Crítico para SVM, ya que es sensible a la escala de las distancias).
* **Modelado:** `SVC` (Support Vector Classifier) de Scikit-Learn.
* **Optimización:** GridSearch para ajuste de hiperparámetros ($C$, $\gamma$, Kernel).

## 📊 Metodología (Plan de Trabajo)
1.  **EDA:** Análisis de correlación y visualización de distribuciones (Violin Plots).
2.  **Preprocessing:** Estandarización de datos (Z-Score normalization).
3.  **Entrenamiento:** Comparación de Kernels (Lineal vs. RBF vs. Polinomial).
4.  **Evaluación:** Matriz de Confusión y Curva ROC, con foco en la métrica Recall.

## 📈 Resultados Preliminares
*[Esta sección se actualizará al finalizar el entrenamiento del modelo]*
* **Accuracy:** [PENDIENTE]
* **Recall (Malignos):** [PENDIENTE]
* **Mejores Hiperparámetros:** [PENDIENTE]

---
*Este proyecto fue desarrollado como parte de un portafolio de Data Science enfocado en la diversificación de algoritmos de Machine Learning.*
