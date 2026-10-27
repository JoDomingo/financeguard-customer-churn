# FinanceGuard — Customer Churn Prediction

Proyecto individual de Machine Learning orientado al análisis y predicción del abandono de clientes bancarios.

El objetivo fue identificar qué clientes presentan mayor probabilidad de abandonar el banco y analizar qué variables están asociadas al churn, combinando modelos supervisados, optimización de hiperparámetros y técnicas de aprendizaje no supervisado.

---

## 📌 Problema de negocio

La pérdida de clientes representa un problema relevante para cualquier entidad financiera, ya que adquirir nuevos clientes suele implicar mayores costos que retener a los existentes.

A partir de información demográfica, financiera y de comportamiento, el proyecto busca:

- identificar patrones asociados al abandono;
- predecir qué clientes presentan mayor riesgo de churn;
- comparar diferentes algoritmos de clasificación;
- segmentar clientes para detectar perfiles con comportamientos similares;
- aportar información útil para estrategias de retención.

---

## 📊 Dataset

El proyecto utiliza un dataset de **10.000 clientes bancarios** con variables relacionadas con:

- información demográfica;
- ubicación geográfica;
- antigüedad como cliente;
- productos contratados;
- saldo;
- actividad;
- tarjeta de crédito;
- salario estimado;
- estado de permanencia o abandono.

La variable objetivo utilizada para los modelos supervisados es:

`Exited`

donde:

- `0` → cliente que permanece;
- `1` → cliente que abandona.

El diccionario de variables se encuentra disponible en:

```text
docs/diccionario_de_variables.xlsx
```

---

## 🗂️ Estructura del proyecto

```text
financeguard-customer-churn/
│
├── data/
│   ├── Churn_Modelling.csv
│   └── Churn_Modelling_Segmentado.csv
│
├── docs/
│   ├── diccionario_de_variables.xlsx
│   └── Reporte_Modelos.pdf
│
├── notebooks/
│   ├── 01_eda_logistic_regression.ipynb
│   ├── 02_gradient_boosting_optimization.ipynb
│   └── 03_unsupervised_learning.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 🔍 1. Análisis exploratorio y modelo baseline

Notebook:

```text
notebooks/01_eda_logistic_regression.ipynb
```

En esta primera etapa se realizó:

- exploración general del dataset;
- análisis de distribuciones y variables;
- revisión de la variable objetivo;
- preprocesamiento de variables numéricas y categóricas;
- codificación mediante One-Hot Encoding;
- escalado de variables;
- separación de datos en entrenamiento y prueba;
- construcción de un modelo base mediante **Regresión Logística**.

La regresión logística se utilizó como baseline para establecer un punto de comparación con modelos más complejos.

### Métricas utilizadas

Se evaluó el desempeño mediante:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC

Además, se analizaron matrices de confusión para comprender los distintos tipos de error del modelo.

---

## 🚀 2. Modelos avanzados y optimización

Notebook:

```text
notebooks/02_gradient_boosting_optimization.ipynb
```

Luego del baseline se entrenaron y compararon diferentes algoritmos de Machine Learning:

- Random Forest
- XGBoost
- LightGBM
- CatBoost
- Stacking Ensemble

Para obtener una evaluación más robusta se utilizó **validación cruzada estratificada**.

También se trabajó con **Optuna** para optimizar hiperparámetros y mejorar el rendimiento de los modelos.

### Evaluación

Además de las métricas tradicionales, se prestó especial atención a:

**PR-AUC (Precision-Recall AUC)**

debido al desbalance existente entre clientes que permanecen y clientes que abandonan.

El modelo de **Stacking** obtuvo aproximadamente:

```text
PR-AUC Cross Validation ≈ 0.71 ± 0.02
PR-AUC Test             ≈ 0.73
```

Tras comparar rendimiento, estabilidad y características de los distintos modelos, **CatBoost fue seleccionado como modelo final del proyecto**.

---

## 🧩 3. Segmentación de clientes

Notebook:

```text
notebooks/03_unsupervised_learning.ipynb
```

Además de predecir el churn, se aplicaron técnicas de aprendizaje no supervisado para estudiar distintos perfiles de clientes.

Se utilizaron:

- K-Means
- DBSCAN
- PCA
- t-SNE

### Objetivo

La segmentación permitió analizar grupos de clientes con características similares y estudiar cómo se distribuye el churn dentro de esos segmentos.

Las técnicas de reducción de dimensionalidad facilitaron la visualización de la estructura de los clusters.

Como resultado de esta etapa se generó:

```text
data/Churn_Modelling_Segmentado.csv
```

que incorpora la información derivada del análisis de segmentación.

---

## 💰 Evaluación orientada al negocio

Además de evaluar los modelos únicamente mediante métricas estadísticas, el proyecto incorporó un análisis del **threshold de clasificación**.

Modificar el threshold permite cambiar el balance entre:

- clientes con riesgo correctamente identificados;
- falsos positivos;
- falsos negativos.

Esto resulta especialmente importante en churn, ya que no todos los errores tienen el mismo impacto económico.

También se trabajó con una matriz de costos para analizar cómo distintas decisiones del modelo pueden afectar una estrategia de retención.

---

## 📈 Principales conclusiones

El proyecto permitió comprobar que:

- el churn puede modelarse mediante información demográfica, financiera y de comportamiento;
- modelos de boosting y ensembles superan al baseline de regresión logística;
- la elección del modelo no debe basarse únicamente en Accuracy;
- PR-AUC resulta especialmente útil ante clases desbalanceadas;
- modificar el threshold puede adaptar el modelo a diferentes objetivos de negocio;
- las técnicas de clustering permiten complementar la predicción individual con una visión segmentada de la cartera de clientes.

---

## 🛠️ Tecnologías utilizadas

### Lenguaje y análisis

- Python
- Pandas
- NumPy

### Machine Learning

- Scikit-learn
- XGBoost
- LightGBM
- CatBoost
- Optuna

### Modelos supervisados

- Logistic Regression
- Random Forest
- Gradient Boosting
- Stacking Ensemble

### Aprendizaje no supervisado

- K-Means
- DBSCAN
- PCA
- t-SNE

### Visualización

- Matplotlib
- Seaborn

---

## 📄 Documentación

El reporte complementario del análisis y comparación de modelos se encuentra disponible en:

```text
docs/Reporte_Modelos.pdf
```

---

## 🎯 Objetivo del proyecto

FinanceGuard fue desarrollado como proyecto integrador de Machine Learning durante mi formación en Data Science.

El trabajo permitió recorrer un flujo completo de análisis:

```text
Exploración de datos
        ↓
Preprocesamiento
        ↓
Modelo baseline
        ↓
Comparación de modelos
        ↓
Optimización
        ↓
Evaluación
        ↓
Segmentación de clientes
        ↓
Interpretación orientada al negocio
```

El foco no estuvo únicamente en obtener el modelo con mejores métricas, sino también en comprender cómo convertir sus resultados en información útil para la toma de decisiones.