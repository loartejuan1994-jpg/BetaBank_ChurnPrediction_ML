🏦 Predicción de Abandono de Clientes — Beta Bank (Churn)
> Modelo de clasificación binaria para predecir si un cliente abandonará el banco, usando técnicas de corrección de desequilibrio de clases y optimización de hiperparámetros.
---
📋 Descripción del Proyecto
Los clientes de Beta Bank se están yendo cada mes. Retener a un cliente existente es más barato que atraer uno nuevo. Este proyecto desarrolla un modelo de Machine Learning que predice qué clientes están en riesgo de abandonar el banco, permitiendo acciones preventivas de retención.
Criterio de aprobación: F1 Score ≥ 0.59 en el conjunto de prueba.
---
🎯 Objetivo
Desarrollar el modelo con el máximo F1 Score posible, midiendo además AUC-ROC como métrica secundaria y comparando ambas métricas en el conjunto de prueba.
---
📁 Estructura del Proyecto
```
Project_11_Prediccion_Abandono_Clientes_BetaBank/
│
├── Project_11_BetaBank_ChurnPrediction.ipynb   # Notebook principal
├── datasets/
│   └── Churn.csv                               # Dataset original
└── README.md
```
---
📊 Dataset
Característica	Descripción
`CreditScore`	Valor de crédito del cliente
`Geography`	País de residencia
`Gender`	Sexo del cliente
`Age`	Edad
`Tenure`	Años con el banco
`Balance`	Saldo de la cuenta
`NumOfProducts`	Productos bancarios utilizados
`HasCrCard`	¿Tiene tarjeta de crédito?
`IsActiveMember`	¿Es miembro activo?
`EstimatedSalary`	Salario estimado
`Exited` ⭐	Variable objetivo — abandonó (1) o no (0)
> `RowNumber`, `CustomerId` y `Surname` fueron eliminadas por no tener valor predictivo.
---
⚙️ Flujo de Trabajo
```
1. Preparación de datos
   ├── Imputación de valores nulos (Tenure → mediana)
   ├── Eliminación de columnas irrelevantes
   ├── Codificación OHE (Geography, Gender)
   └── Escalado StandardScaler

2. Análisis del desequilibrio de clases
   ├── Clase 0 (No abandona): ~79.7%
   ├── Clase 1 (Abandona):    ~20.3%
   └── Ratio: 3.92:1

3. Corrección del desequilibrio
   ├── Enfoque 1 → class_weight='balanced'
   ├── Enfoque 2 → Oversampling (SMOTE / Aleatorio)
   └── Enfoque 3 → Undersampling

4. Selección del mejor modelo
   └── Comparativa F1 Score en validación

5. Prueba final
   ├── F1 Score en test
   ├── AUC-ROC + Curva ROC
   ├── Matriz de confusión
   └── Importancia de variables
```
---
🤖 Modelos Evaluados
Modelo	Enfoque	F1 Score (Validación)
Random Forest ⭐	Oversampling	~60%
Random Forest	class_weight	~56%
Árbol de Decisión	class_weight	~56%
Modelo Base	Sin corrección	~55%
Random Forest	Undersampling	~54%
Regresión Logística	class_weight	~48%
---
📈 Resultados Finales
Métrica	Resultado
F1 Score (test)	≥ 0.59 ✅
AUC-ROC (test)	≥ 0.85
¿Cumple el umbral?	SÍ ✅
Variables más importantes para predecir el abandono:
```
Age               → ~31%  ← más determinante
NumOfProducts     → ~19%
Balance           → ~12%
EstimatedSalary   →  ~9%
CreditScore       →  ~8%
IsActiveMember    →  ~6%
```
---
🛠️ Tecnologías Utilizadas
![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas)
![Scikit--learn](https://img.shields.io/badge/Scikit--learn-1.x-F7931E?logo=scikit-learn)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-11557C)
![Seaborn](https://img.shields.io/badge/Seaborn-0.x-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter)
---
🚀 ¿Cómo ejecutar el proyecto?
```bash
# 1. Clona el repositorio
git clone https://github.com/tu_usuario/betabank-churn-prediction.git

# 2. Instala las dependencias
pip install pandas numpy scikit-learn matplotlib seaborn imbalanced-learn

# 3. Abre el notebook
jupyter notebook Project_11_BetaBank_ChurnPrediction.ipynb
```
---
💡 Conclusiones Clave
El desequilibrio de clases (3.92:1) impacta significativamente el F1 Score si no se corrige.
El Bosque Aleatorio con Oversampling fue el mejor modelo, superando el umbral de 0.59.
La edad del cliente es el factor más determinante para predecir el abandono (~31%).
El AUC-ROC fue superior al F1 Score, lo que es típico en datasets desbalanceados donde el modelo discrimina bien globalmente pero tiene dificultades con la clase minoritaria.
Los Falsos Negativos son el error más costoso para Beta Bank — clientes que abandonan sin ser detectados.
---
📌 Recomendaciones para Beta Bank
Priorizar clientes de mayor edad con pocos productos activos e inactividad reciente.
Ajustar el umbral de decisión por debajo de 0.50 para capturar más Falsos Negativos.
Reentrenar el modelo cada 6 meses con datos actualizados.
Monitorear las variables `Age`, `NumOfProducts` e `IsActiveMember` como señales tempranas de riesgo.
---
👤 Autor
Juan — Junior Data Scientist | Geology & Mining Engineer  
Proyecto desarrollado como parte del programa Data Scientist — TripleTen
---
Sprint 11 — Aprendizaje Supervisado
