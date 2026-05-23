# Predicción del Riesgo de Hipertensión

Proyecto de ciencia de datos orientado a predecir si un paciente presenta riesgo de hipertensión a partir de variables clínicas y de estilo de vida.  
El análisis se desarrolla en el notebook `riesgo_hipertension.ipynb`, donde se realiza exploración de datos, preparación de variables, entrenamiento de modelos, evaluación e interpretación de resultados.

---

## Objetivo del proyecto

Construir y comparar modelos de clasificación supervisada capaces de predecir la variable objetivo `Hipertension`, utilizando información clínica como edad, colesterol, glucosa, índice de masa corporal, nivel de estrés, duración del sueño, antecedentes familiares y otros factores asociados.

El proyecto busca no solo obtener un buen desempeño predictivo, sino también interpretar qué condiciones pueden estar relacionadas con un mayor riesgo de hipertensión.

---

## Archivos del repositorio

| Archivo | Descripción |
|---|---|
| `Datos_hipertension.csv` | Conjunto de datos utilizado para el entrenamiento y evaluación de los modelos. |
| `Diccionario_Datos.xlsx` | Diccionario con la descripción de las variables del dataset. |
| `riesgo_hipertension.ipynb` | Notebook principal con el desarrollo completo del proyecto. |

---

## Variables utilizadas

El conjunto de datos contiene variables numéricas y categóricas relacionadas con el estado de salud del paciente.

### Variables numéricas

- `Edad`
- `Ingesta_Sal`
- `Nivel_Stres`
- `Colesterol`
- `Duración_Sueño`
- `BMI`
- `Glucosa`

### Variables categóricas

- `Medicación`
- `Historia_Familiar`
- `Actividad_Fisica`
- `Fumador`
- `Enfermedad_Corazon`

### Variable objetivo

- `Hipertension`: indica si el paciente presenta o no hipertensión.

---

## Flujo de trabajo

El notebook sigue un flujo completo de ciencia de datos:

1. **Importación de librerías**
   - `pandas`
   - `numpy`
   - `matplotlib`
   - `scikit-learn`

2. **Carga del conjunto de datos**
   - Lectura del archivo `Datos_hipertension.csv`.

3. **Exploración inicial**
   - Revisión de las primeras filas.
   - Identificación de tipos de datos.
   - Análisis de variables numéricas y categóricas.
   - Revisión de valores atípicos.
   - Verificación de estructura del dataset.

4. **Preparación de datos**
   - Separación entre variables predictoras y variable objetivo.
   - División en datos de entrenamiento y prueba.
   - Codificación de variables categóricas con `OneHotEncoder`.
   - Escalamiento de variables numéricas para el modelo KNN.
   - Construcción de pipelines de procesamiento y modelado.

5. **Entrenamiento de modelos**
   - Árbol de Decisión.
   - K-Vecinos más Cercanos, KNN.

6. **Optimización de hiperparámetros**
   - Uso de `GridSearchCV`.
   - Validación cruzada con `KFold`.

7. **Evaluación**
   - Accuracy.
   - Precision.
   - Recall.
   - F1-score.
   - Matriz de confusión.

8. **Interpretabilidad**
   - Extracción de importancia de variables.
   - Generación de reglas interpretables del Árbol de Decisión.

9. **Estimación de confianza**
   - Intervalo de confianza del 95% mediante bootstrapping para evaluar estabilidad del modelo.

---

## Modelos implementados

### Árbol de Decisión

Se entrenó un modelo `DecisionTreeClassifier` dentro de un pipeline.  
La búsqueda de hiperparámetros evaluó diferentes combinaciones de:

- Criterio de división: `gini` y `entropy`.
- Profundidad máxima del árbol.
- Mínimo de muestras requeridas para dividir un nodo.

El mejor modelo de Árbol de Decisión utilizó:

```python
criterion = "entropy"
max_depth = 6
min_samples_split = 3
```

### K-Vecinos más Cercanos, KNN

Se entrenó un modelo `KNeighborsClassifier` utilizando escalamiento de variables numéricas y codificación de variables categóricas.

La búsqueda de hiperparámetros evaluó:

- Número de vecinos.
- Tipo de escalador:
  - `StandardScaler`
  - `MinMaxScaler`
  - `RobustScaler`

El mejor modelo KNN utilizó:

```python
n_neighbors = 5
scaler = StandardScaler()
```

---

## Resultados principales

| Modelo | Accuracy | Precision clase 1 | Recall clase 1 | F1-score clase 1 |
|---|---:|---:|---:|---:|
| Árbol de Decisión | 0.90 | 0.94 | 0.88 | 0.91 |
| KNN | 0.89 | 0.95 | 0.83 | 0.89 |

El Árbol de Decisión presentó el mejor desempeño general, con una exactitud aproximada del 90%. Además, permite interpretar las reglas de decisión utilizadas para clasificar a los pacientes.

---

## Interpretación general

El modelo de Árbol de Decisión identificó variables como `Colesterol`, `Glucosa`, `BMI`, `Historia_Familiar`, `Fumador` y `Enfermedad_Corazon` como factores relevantes dentro de las reglas de clasificación.

Algunas reglas muestran que niveles altos de colesterol y glucosa pueden estar asociados con una mayor probabilidad de clasificar a un paciente como hipertenso.

Este tipo de modelo es útil porque combina desempeño predictivo con interpretabilidad, permitiendo entender bajo qué condiciones el algoritmo considera que un paciente puede estar en riesgo.

---

## Tecnologías utilizadas

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Scikit-learn

---

## Cómo ejecutar el proyecto

1. Clonar el repositorio:

```bash
git clone https://github.com/JuanMarin58/Prediccion_del_riesgo_de_hipertension.git
```

2. Entrar a la carpeta del proyecto:

```bash
cd Prediccion_del_riesgo_de_hipertension
```

3. Instalar las dependencias principales:

```bash
pip install pandas numpy matplotlib scikit-learn openpyxl jupyter
```

4. Abrir Jupyter Notebook:

```bash
jupyter notebook
```

5. Ejecutar el archivo:

```text
riesgo_hipertension.ipynb
```

---

## Conclusiones

El proyecto demuestra cómo aplicar técnicas de aprendizaje automático para clasificar el riesgo de hipertensión usando variables clínicas y de estilo de vida.

El Árbol de Decisión obtuvo el mejor desempeño general y ofrece una ventaja importante frente a KNN: permite interpretar las reglas de clasificación. Esto es especialmente valioso en problemas de salud, donde no basta con predecir, sino que también es importante comprender los factores que influyen en la decisión del modelo.

Este modelo debe entenderse como una herramienta académica y exploratoria de apoyo al análisis de datos, no como un sistema de diagnóstico médico.

---

## Autor

Proyecto desarrollado por Juan Carlos Marin.
