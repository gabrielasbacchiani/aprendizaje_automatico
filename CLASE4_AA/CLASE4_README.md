# Clase 4 – Aprendizaje Automático: Aprendizaje Supervisado

Repositorio con las actividades de la Clase 4: regresión lineal y regresión logística.

## Contenido del repositorio

- `Clase4_AA_2026.ipynb` — Actividad 1: regresión lineal
- `Regresion_logistica.ipynb` — Actividad 2: regresión logística
- `dataset/academic_survival_longitudinal.csv` — dataset usado en la Actividad 1
- `dataset/Actividad2_usuarios_win_mac_lin.csv` — dataset usado en la Actividad 2 (provisto por la cátedra)

## Actividad 1: Regresión lineal

**Objetivo:** predecir el promedio del semestre (`Sem_GPA`) de un estudiante a partir de variables académicas y socioeconómicas.

**Dataset:** [Student Retention and Academic Performance Data](https://www.kaggle.com/datasets/razanihababdellatif/student-retention-and-academic-performance-data) (Kaggle). Contiene 79.239 registros longitudinales de 20.000 estudiantes (una fila por estudiante y semestre), con variables como asistencia, horas de trabajo, ingreso familiar, estrés financiero, materias desaprobadas, visitas de tutoría, entre otras.

**Proceso:**
1. Carga y primera exploración de los datos
2. Análisis exploratorio (AED): distribución de la variable objetivo, detección de valores atípicos y correlaciones con las posibles predictoras
3. Limpieza: corrección de valores de asistencia fuera de rango (0–100%) e imputación de valores faltantes con la mediana
4. Selección de variables predictoras según su correlación con el promedio
5. División en conjuntos de entrenamiento (80%) y prueba (20%)
6. Entrenamiento de un modelo de regresión lineal (`scikit-learn`)
7. Evaluación con error absoluto medio, error cuadrático medio, error absoluto mediano, varianza explicada y R²

**Resultado:** R² ≈ 0,36 y error absoluto medio ≈ 0,26 puntos de promedio (escala 0–4). El modelo captura una tendencia real pero moderada; el detalle de la interpretación está en la conclusión del notebook.

### Glosario de variables (dataset de la Actividad 1)

| Columna | En español | Qué significa |
|---|---|---|
| `Student_ID` | ID del estudiante | Identificador (se repite: hay una fila por semestre) |
| `Age` | Edad | |
| `Gender` | Género | |
| `First_Generation` | Primera generación | 1 = es el primero de su familia en ir a la universidad |
| `Family_Income` | Ingreso familiar | |
| `Household_Size` | Tamaño del hogar | Cantidad de personas que viven juntas |
| `Housing_Status` | Situación de vivienda | Por ejemplo, si vive con su familia o solo |
| `Scholarship` | Beca | 1 = tiene beca, 0 = no |
| `Tuition_Base` | Arancel base | Costo de cursar |
| `Semester` | Semestre | Número de semestre que cursa (1 a 8) |
| `Course_Load` | Carga de materias | Cuánto cursa en el semestre |
| `Work_Hours` | Horas de trabajo | Probablemente por semana |
| `Emergency_Expense` | Gasto de emergencia | Gastos imprevistos |
| `Sem_GPA` | Promedio del semestre | **Variable objetivo de la Actividad 1** |
| `Attendance` | Asistencia | Porcentaje de asistencia a clases |
| `LMS_Logins` | Ingresos al campus virtual | LMS = plataforma educativa online |
| `Advising_Visits` | Visitas de tutoría | Consultas con un asesor académico |
| `Failed_Courses` | Materias desaprobadas | |
| `Financial_Stress` | Estrés financiero | Nivel de presión económica |
| `Target_Dropout_Next_Sem` | Abandono el próximo semestre | 1 = abandonó, 0 = siguió (no se usó en esta actividad) |
| `End_of_Semester_Status` | Estado a fin de semestre | Enrolled = cursando, Dropped_Out = abandonó, Graduated = se graduó |
| `Censored` | Dato censurado | Se dejó de seguir al estudiante, no sabemos qué pasó después |

## Actividad 2: Regresión logística

**Objetivo:** predecir qué sistema operativo (Windows, Macintosh o Linux) usa un usuario que visita un sitio web, a partir de cuatro variables de comportamiento tomadas de Google Analytics: duración de la visita, cantidad de páginas vistas, cantidad de acciones realizadas y la suma del valor de esas acciones.

**Dataset:** `Actividad2_usuarios_win_mac_lin.csv`, provisto por la cátedra. Contiene 170 registros sin valores faltantes, con la variable objetivo codificada como:
- 0 = Windows (86 casos)
- 1 = Macintosh (40 casos)
- 2 = Linux (44 casos)

**Proceso:**
1. Carga y exploración de los datos (incluye un gráfico de dispersión coloreado por clase)
2. Definición de X (las 4 variables de comportamiento) e Y (la clase)
3. División en entrenamiento (80%) y prueba (20%), mezclando los datos al azar antes de cortar
4. Entrenamiento de un clasificador de regresión logística (`scikit-learn`, `LogisticRegression`)
5. Evaluación con accuracy, matriz de confusión y reporte de clasificación (precisión, recall y f1-score por clase)

**Resultado:** el modelo alcanzó un **accuracy del 79%** sobre el conjunto de prueba. Clasificó perfectamente a los usuarios de Linux (precisión 0,88, recall 1,00), mientras que los errores se concentraron entre Windows y Macintosh, las dos clases que se veían más mezcladas en el gráfico de dispersión. El detalle completo del análisis está en la conclusión del notebook.

## Cómo ejecutar los notebooks

Los notebooks están pensados para correr en [Google Colab](https://colab.research.google.com/):

1. Abrir el archivo `.ipynb` en Colab (subiéndolo o desde GitHub con *Open in Colab*).
2. Ejecutar las celdas en orden (*Entorno de ejecución → Ejecutar todas*).
3. El CSV de la Actividad 1 se lee directamente desde este repositorio, así que no hace falta subir ningún archivo a mano.

## Herramientas utilizadas

- Python
- pandas / numpy
- matplotlib
- scikit-learn

## Autora

Gabriela Bacchiani
