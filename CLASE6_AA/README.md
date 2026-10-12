# Predicción de abandono y éxito académico: regresión logística vs. árbol de decisión

Trabajo práctico de la materia **Aprendizaje Automático**

Se comparan dos modelos de clasificación supervisada para predecir si un estudiante universitario **se gradúa, abandona o sigue matriculado**.

- 📓 **Notebook:** CLASE6_AA/NOTEBOOKS/CLASE6_AA.ipynb
- 🎥 **Video (5 min):** https://drive.google.com/drive/folders/1y0jpGvSrdDd6ti7K2u5pDwJ1y-dmvpYH?usp=drive_link

## Problema

Predecir la variable `target` (3 clases: `Graduate`, `Dropout`, `Enrolled`) a partir de datos de matrícula, situación económica y rendimiento académico de los primeros dos semestres. Es un problema de **clasificación multiclase**.

## Dataset

[*Predict Students' Dropout and Academic Success*](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success) (UCI Machine Learning Repository / Kaggle).

| Característica | Detalle |
| --- | --- |
| Estudiantes | 4.424 |
| Variables predictoras | 36 |
| Tipos | 18 numéricas, 10 categóricas (códigos), 8 binarias |
| Valores nulos / duplicados | ninguno |
| Archivo en este repo | CLASE6_AA/DATASETS/students_dropout_academic_success.csv |

## Metodología

1. Análisis exploratorio, con foco en la situación económica (beca, deuda, cuotas al día): tablas cruzadas, chi-cuadrado y V de Cramér.
2. División estratificada 80 % entrenamiento / 20 % prueba (`random_state=42`).
3. Preprocesamiento con `Pipeline` + `ColumnTransformer`: One-Hot Encoding para las categóricas y `StandardScaler` para las numéricas (solo en la regresión logística).
4. Dos modelos, ajustados con `GridSearchCV` (validación cruzada estratificada de 5 folds, métrica F1 macro):

| Modelo | Hiperparámetros evaluados | Mejor combinación |
| --- | --- | --- |
| Regresión logística | `C` ∈ {0.01, 0.1, 1, 10} | `C = 1` |
| Árbol de decisión | `max_depth` ∈ {3, 4, 5, 6, 8, 10}, `min_samples_leaf` ∈ {1, 5, 10, 20} | `max_depth = 8`, `min_samples_leaf = 20` |

5. Evaluación en el conjunto de prueba: accuracy, precision, recall, F1 y matriz de confusión.
6. Interpretación: importancia de variables (árbol) y coeficientes (regresión logística).

## Resultados (conjunto de prueba)

| Métrica | Regresión logística | Árbol de decisión |
| --- | --- | --- |
| Accuracy | **0,768** | 0,733 |
| F1 macro | **0,696** | 0,656 |
| Recall Graduate | **0,912** | 0,878 |
| Recall Dropout | **0,754** | 0,718 |
| Recall Enrolled | **0,396** | 0,358 |

- El árbol sin ajustar sobreajustó (accuracy 1,00 en entrenamiento vs. 0,68 en prueba). Con `max_depth=8` y `min_samples_leaf=20` pasó a 0,79 vs. 0,73.
- Las variables más relevantes en ambos modelos: unidades curriculares aprobadas en el 2.º semestre y tener las cuotas al día.
- En el análisis exploratorio, el abandono fue de 87 % entre quienes tenían cuotas atrasadas contra 25 % entre quienes estaban al día (V de Cramér = 0,43). Es una **asociación, no una causalidad**.

## Conclusión

La **regresión logística** resuelve mejor el problema: supera al árbol en todas las métricas y generaliza mejor. El árbol es más fácil de explicar con reglas, pero rindió menos. Ambos modelos tienen dificultad para identificar a los estudiantes `Enrolled`.

## Cómo ejecutar

1. Abrir el notebook en Google Colab (o Jupyter).
2. Ejecutar **Entorno de ejecución → Ejecutar todo**. El notebook carga el dataset directamente desde este repositorio.
3. Librerías: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn`.


## Autora

Gabriela Bacchiani, [@gabrielasbacchiani](https://github.com/gabrielasbacchiani)
