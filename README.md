# Predicción de reingreso hospitalario en pacientes diabéticos

Este repositorio contiene el código desarrollado para el proyecto final de la asignatura **Aprendizaje Avanzado**, centrado en la aplicación de técnicas de aprendizaje automático sobre el dataset **Diabetes 130-US Hospitals for years 1999-2008**.

El objetivo principal es predecir el reingreso hospitalario de pacientes diabéticos y analizar varias problemáticas relevantes en un contexto real de aplicación sanitaria.

El trabajo no se limita a entrenar modelos predictivos, sino que estudia también aspectos importantes para el despliegue responsable de sistemas de Machine Learning en salud, como el desbalanceo de clases, el sesgo, la privacidad y la explicabilidad.

---

## Objetivo del proyecto

El objetivo es construir y evaluar modelos de clasificación capaces de predecir la variable `readmitted`, que indica si un paciente diabético fue readmitido tras el alta hospitalaria.

A partir de este problema se analizan cuatro problemáticas principales:

1. **Desbalanceo de clases**: la distribución de la variable objetivo no es uniforme, lo que puede afectar al aprendizaje de los modelos.
2. **Sesgo y fairness**: se estudia si el comportamiento del modelo varía entre grupos de pacientes.
3. **Privacidad**: se simula un escenario de aprendizaje federado, donde los datos no se centralizan.
4. **Explicabilidad**: se utilizan técnicas XAI para interpretar las predicciones del modelo.

---

## Dataset

El dataset utilizado es **Diabetes 130-US Hospitals for years 1999-2008**, disponible en UCI Machine Learning Repository.

Contiene información de ingresos hospitalarios de pacientes diabéticos en hospitales de Estados Unidos, incluyendo variables demográficas, diagnósticas y clínicas.

La variable objetivo principal es:

```text
readmitted
```

Esta variable indica si el paciente fue readmitido tras el alta hospitalaria.

Los archivos de datos utilizados en el proyecto se encuentran en la carpeta `data/`:

```text
data/
├── diabetic_data.csv
├── IDS_mapping.csv
└── diabetes_preprocesado.csv
```

Los archivos `diabetic_data.csv` e `IDS_mapping.csv` corresponden al dataset original. El archivo `diabetes_preprocesado.csv` se genera tras ejecutar el notebook de preprocesamiento.

---

## Estructura del repositorio

La estructura principal del proyecto es la siguiente:

```text
PROYECTO_DIABETES/
├── .vscode/
│   └── settings.json
├── data/
│   ├── diabetic_data.csv
│   ├── IDS_mapping.csv
│   └── diabetes_preprocesado.csv
├── notebooks/
│   ├── 01_desbalanceo.ipynb
│   ├── 02_SesgoFairness.ipynb
│   ├── 03_privacidad.ipynb
│   ├── 04_Xai.ipynb
│   ├── arbol_decision.ipynb
│   ├── eda.ipynb
│   ├── gradient_boosting.ipynb
│   ├── preprocesamiento.ipynb
│   ├── problematicas.ipynb
│   └── random_forest.ipynb
├── outliers/
├── visualizacion_gradient_boosting/
│   └── xgboost_importancia_top10.png
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

---

## Descripción de los notebooks

### `notebooks/eda.ipynb`

Contiene el análisis exploratorio inicial del dataset. Se estudian las dimensiones del conjunto de datos, los tipos de variables, la presencia de valores ausentes, la distribución de la variable objetivo y las primeras visualizaciones del problema.

### `notebooks/preprocesamiento.ipynb`

Incluye la limpieza y transformación de los datos antes del entrenamiento de los modelos. En este notebook se tratan valores ausentes, se codifican variables categóricas y se prepara una versión procesada del dataset.

Este notebook genera el archivo:

```text
data/diabetes_preprocesado.csv
```

Este archivo es utilizado por los notebooks posteriores.

### `notebooks/arbol_decision.ipynb`

Entrena y evalúa modelos basados en árboles de decisión. Primero se analiza un árbol sin restricciones, observando su tendencia al sobreajuste, y después se aplica pre-poda mediante búsqueda de hiperparámetros.

### `notebooks/random_forest.ipynb`

Evalúa modelos Random Forest como método de ensamblado basado en árboles. Se realiza búsqueda de hiperparámetros y se comparan los resultados obtenidos con los del árbol de decisión.

### `notebooks/gradient_boosting.ipynb`

Compara modelos de boosting, incluyendo AdaBoost, Gradient Boosting y XGBoost. A partir de estos experimentos se selecciona XGBoost como modelo baseline principal del proyecto.

### `notebooks/01_desbalanceo.ipynb`

Analiza la problemática del desbalanceo de clases. Se aplica SMOTE sobre el conjunto de entrenamiento para equilibrar las clases y se comparan varios modelos con esta técnica.

### `notebooks/02_SesgoFairness.ipynb`

Estudia la presencia de posibles diferencias de comportamiento del modelo entre grupos de pacientes. Se calculan métricas relacionadas con fairness para analizar si los errores del modelo afectan de forma desigual a determinados grupos.

### `notebooks/03_privacidad.ipynb`

Implementa la parte relacionada con privacidad y aprendizaje federado. Se prueban distintas alternativas y se desarrolla una simulación de Federated Learning con XGBoost.

En esta simulación, varios clientes representan hospitales distintos que colaboran en el entrenamiento de un modelo sin centralizar directamente los datos.

### `notebooks/04_Xai.ipynb`

Contiene el análisis de explicabilidad del modelo mediante técnicas como SHAP y LIME. El objetivo es interpretar qué variables influyen más en las predicciones y analizar el comportamiento del modelo tanto de forma global como local.

---

## Instalación y ejecución

Esta sección describe los pasos necesarios para ejecutar el proyecto desde cero.

### 1. Clonar o descargar el repositorio

Clonar el repositorio desde GitHub:

```bash
git clone https://github.com/efc37/proyecto_diabetes.git
```

### 2. Comprobar la carpeta de datos

Antes de ejecutar los notebooks, comprobar que la carpeta `data/` contiene los archivos originales:

```text
data/diabetic_data.csv
data/IDS_mapping.csv
```

El archivo:

```text
data/diabetes_preprocesado.csv
```

se genera al ejecutar el notebook:

```text
notebooks/preprocesamiento.ipynb
```

Si `diabetes_preprocesado.csv` no existe, debe ejecutarse primero el notebook de preprocesamiento.

### 3. Instalar las dependencias

Una vez se dispone de los datos necesarios, se deben instalar las librerías necesarias:

```bash
pip install -r requirements.txt
```

El archivo `requirements.txt` contiene las dependencias principales del proyecto.


### 4. Ejecutar los notebooks desde Visual Studio Code

El proyecto puede ejecutarse directamente desde **Visual Studio Code**.

Para ello, abrir la carpeta raíz del proyecto en Visual Studio Code y ejecutar los diferentes notebooks según el orden recomendado.


## Orden recomendado de ejecución

Para reproducir el proyecto completo desde cero, se recomienda ejecutar los notebooks en el siguiente orden.

### 1. Análisis exploratorio

```text
notebooks/eda.ipynb
```

### 2. Preprocesamiento

```text
notebooks/preprocesamiento.ipynb
```

Este notebook genera el archivo:

```text
data/diabetes_preprocesado.csv
```

Este archivo es necesario para los notebooks posteriores.

### 3. Modelos baseline

Ejecutar los siguientes notebooks:

```text
notebooks/arbol_decision.ipynb
notebooks/random_forest.ipynb
notebooks/gradient_boosting.ipynb
```

### 4. Problemática 1: desbalanceo

```text
notebooks/01_desbalanceo.ipynb
```

### 5. Problemática 2: sesgo y fairness

```text
notebooks/02_SesgoFairness.ipynb
```


### 6. Problemática 3: privacidad

```text
notebooks/03_privacidad.ipynb
```


### 7. Problemática 4: explicabilidad

```text
notebooks/04_Xai.ipynb
```
---

## Reproducibilidad

Para favorecer la reproducibilidad, los notebooks utilizan semillas aleatorias (42) en las particiones de datos, validación cruzada, modelos y técnicas de remuestreo.

Además, las divisiones `train/test` se realizan de forma estratificada para mantener la distribución original de la variable objetivo `readmitted`.

---

## Autores
Sara Mora García, Elena Fernández Cebrián y Joël Expósito Bajo
Proyecto realizado para la asignatura **Aprendizaje Avanzado**.