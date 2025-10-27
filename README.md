# Sprint 10 – Predicción de Pérdida de Clientes (*Churn Prediction*)

**Proyecto del Sprint 10 del Bootcamp de Data Science**  
Autora: *Diana Marlene Reyes Fraire*  

---
Sprint10_Churn/
├── data/
│ └── Churn.csv # Dataset original
├── notebooks/
│ └── sprint10_churn_prediction.ipynb
├── requirements.txt
└── README.md

---

## Metodología

1. **Exploración de datos (EDA)**  
   - El dataset contiene 10,000 registros y 14 columnas.  
   - La variable objetivo es `Exited` (1 = cliente se fue, 0 = cliente permanece).  
   - Las variables `RowNumber`, `CustomerId` y `Surname` fueron eliminadas por no aportar valor predictivo.

2. **Preparación de características**
   - Normalización de nombres de columnas.  
   - Conversión de variables numéricas y categóricas.  
   - Escalado de variables numéricas (`StandardScaler`).  
   - Codificación *One-Hot Encoding* para variables categóricas.

3. **División de datos**
   - Train: 70%  
   - Validation: 15%  
   - Test: 15%  
   - Estratificación aplicada para mantener la proporción de clases (80% vs 20%).

4. **Manejo del desbalance de clases**
   - Modelos con ponderación de clases (`class_weight='balanced'`).  
   - Oversampling y undersampling para comparar efectos.

5. **Evaluación de modelos**
   - Métricas: F1-score (objetivo ≥ 0.59) y AUC-ROC.  
   - Curvas F1 vs Threshold y ROC-AUC para interpretar rendimiento.

---

## Comparativa de Modelos

| Modelo | F1@0.50 | AUC-ROC | Best F1 | Umbral | TP | FN | Comentario |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--|
| Logistic Regression (baseline) | 0.272 | 0.737 | 0.472 | 0.27 | 147 | 131 | Muy sesgado hacia la clase mayoritaria. |
| Logistic Regression (weighted) | 0.463 | 0.739 | 0.477 | 0.58 | 152 | 126 | Mejor equilibrio; ligera mejora del recall. |
| Oversampling | 0.463 | 0.739 | 0.476 | 0.60 | 145 | 133 | Rendimiento similar al ponderado. |
| Undersampling | 0.456 | 0.738 | 0.479 | 0.63 | 138 | 140 | Reduce sesgo, pero pierde precisión. |
| Random Forest (balanced) | 0.596 | 0.848 | 0.625 | 0.60 | 159 | 119 | Modelo no lineal; gran mejora en F1 y AUC. |
| **Random Forest (optimizado)** | **0.605** | **0.856** | **0.605** | **0.50** | **168** | **110** | ✅ Cumple meta del proyecto (F1 ≥ 0.59) y generaliza mejor. |

---

## Conclusiones Técnicas

- El modelo **Random Forest optimizado** alcanzó un **F1-score de 0.6054** y un **AUC-ROC de 0.8563** en el conjunto de prueba.  
- Cumple con el objetivo del proyecto y mantiene una excelente capacidad de generalización.  
- Aunque el modelo ponderado detectó ligeramente más abandonos (mayor recall), el Random Forest ofrece un **mejor equilibrio entre precisión y recall**, con un umbral estándar de 0.5.  
- Esto lo convierte en un modelo más estable y confiable para su implementación práctica.

---

## Resumen Ejecutivo

El proyecto tiene como objetivo predecir la pérdida de clientes (*churn*) en una institución financiera, con el fin de ayudar al equipo de negocio a implementar estrategias de retención más efectivas.  

Tras entrenar y comparar distintos modelos de Machine Learning, el **modelo final seleccionado** fue un **Random Forest optimizado**, el cual alcanzó un **F1-score de 0.605** y un **AUC-ROC de 0.856** en el conjunto de prueba.  
Estos valores superan la meta establecida del proyecto (F1 ≥ 0.59) y demuestran una **capacidad sólida para generalizar en datos nuevos**.

### Principales hallazgos
- El modelo logra un **equilibrio entre precisión (0.61)** y **recall (0.60)**, lo que significa que puede **identificar correctamente alrededor del 60% de los clientes propensos a abandonar**.  
- La métrica **AUC-ROC = 0.856** indica una excelente capacidad para distinguir entre clientes que permanecen y los que abandonan.  
- Su umbral de decisión estándar (0.5) refleja un **comportamiento estable y sin sesgo hacia ninguna clase**, lo que facilita su uso en entornos reales sin necesidad de ajustes adicionales.

### Conclusión
El modelo **Random Forest optimizado** se considera la mejor solución entre las alternativas evaluadas.  
Permite priorizar a los clientes con mayor riesgo de abandono, proporcionando información clave para **campañas de retención personalizadas** y **acciones preventivas de fidelización**.

### Próximos pasos sugeridos
- Implementar el modelo en un entorno de prueba (*pilot deployment*) para validar su impacto en estrategias reales de retención.  
- Analizar la **importancia de las variables** para comprender qué factores influyen más en el abandono.  
- Explorar modelos basados en *gradient boosting* (XGBoost o LightGBM) para futuras iteraciones.

---

## Requisitos

Para reproducir este proyecto:
```bash
pip install -r requirements.txt