
# 🚗 Detección de Fraude en Seguros de Automóviles

Este proyecto tiene como objetivo identificar posibles fraudes en reclamos de seguros de automóviles utilizando técnicas de Machine Learning. Se emplean varios modelos, se tratan los datos desbalanceados, y se optimizan hiperparámetros para mejorar el desempeño.

---

## 📌 1. Selección de Características

```python
features = [ ... ]
```

Se define una lista de características que serán utilizadas como variables predictoras. Estas incluyen variables ordinales, categóricas codificadas (one-hot) y binarias.

---

## 🧠 2. Modelos de Clasificación

```python
model1 = DecisionTreeClassifier(...)
model2 = KNeighborsClassifier()
model3 = XGBClassifier(...)
model4 = SVC(...)
```

Se crean cuatro modelos de clasificación distintos para luego integrarlos en un ensamblado con VotingClassifier:
- Árbol de decisión
- K-Vecinos más cercanos
- XGBoost (modelo base robusto)
- SVM (con probabilidades activadas)

---

## 🤖 3. Ensamblado con VotingClassifier

```python
voting_clf = VotingClassifier(estimators=[...], voting='soft')
```

Se construye un modelo de ensamblado que utiliza votación **soft**, lo que significa que se consideran las probabilidades de predicción de cada modelo para hacer una predicción final. Esto tiende a mejorar el rendimiento si los modelos base son diversos.

---

## 📊 4. Evaluación Inicial de Modelos

```python
classification_report(...)
```

Se evalúan individualmente los modelos dentro del ensamble utilizando el conjunto de entrenamiento. Se imprime la precisión, recall y F1-score para entender cómo se comportan con datos desbalanceados (clase minoritaria: fraude).

---

## ⚖️ 5. Manejo del Desbalanceo

```python
smote = SMOTE(...)
X_resampled, y_resampled = smote.fit_resample(...)
```

Se utiliza SMOTE para sobresamplear la clase minoritaria (fraude). Esto busca mejorar la capacidad del modelo para aprender patrones de esta clase y reducir falsos negativos.

---

## ⚙️ 6. Ajuste de Hiperparámetros con GridSearchCV

```python
grid_search = GridSearchCV(...)
```

Se entrena un modelo **XGBoost** ajustando automáticamente sus hiperparámetros con `GridSearchCV`, optimizando para el F1-score macro. Se calcula `scale_pos_weight` para ajustar el desequilibrio de clases.

---

## 🧪 7. Evaluación del Modelo Óptimo

```python
classification_report(...)
```

Con los mejores parámetros, se evalúa el modelo sobre el conjunto de validación. Se ajusta el umbral de clasificación (`0.35`) para mejorar el recall de la clase minoritaria.

---

## 📈 8. Importancia de Características

```python
importances = best_model.feature_importances_
```

Se identifican las variables más influyentes en las predicciones del modelo, lo cual ayuda a interpretar cómo toma decisiones el modelo y a posibles mejoras del dataset.

---

## 📉 9. Matriz de Confusión

```python
confusion_matrix(...)
ConfusionMatrixDisplay(...).plot()
```

Se visualiza la matriz de confusión para evaluar el rendimiento en términos de verdaderos positivos/negativos y falsos positivos/negativos. Útil para ver errores de clasificación en detalle.

---

## 🚀 Requisitos

- Python 3.8+
- scikit-learn
- imbalanced-learn
- xgboost
- pandas
- matplotlib

---

## 👩‍💻 Autor

**Pamela Romero**  
Especialista en Costos | Apasionada por el análisis de datos y el aprendizaje automático.

---
