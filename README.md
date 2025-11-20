# TRABAJO N°3 - MODELOS AVANZADOS

## Descripción del Proyecto

Este trabajo analiza los factores macroeconómicos que influyen en las expectativas económicas en Perú, determinando si son optimistas (>50) o pesimistas (≤50). Se construye sobre el trabajo anterior donde se compararon modelos OLS y Logit, expandiendo el análisis con nuevas variables, técnicas de reducción de dimensionalidad y modelos de clasificación avanzados.

## Objetivos

- Incluir nuevas variables (rezagos, variaciones, transformaciones e interacciones)
- Aplicar PCA para entender la estructura de los datos
- Comparar tres modelos de clasificación: Logit, Random Forest y XGBoost
- Tratar el desbalance de clases y evaluar métricas clave
- Utilizar costos para falsos positivos y falsos negativos
- Definir un umbral de decisión óptimo

## Dataset

**Archivo:** `dataset_bcrp_limpio.csv`

**Variables principales:**
- `Fecha`: Fecha mensual (2015-2025)
- `Tasa_Referencia_PM`: Tasa de referencia del banco central
- `Expectativas_Economia`: Indicador de expectativas económicas
- `Tipo_Cambio_Promedio`: Tipo de cambio promedio
- `PBI_Mensual`: Producto Bruto Interno mensual
- `IPC`: Índice de Precios al Consumidor

**Variable objetivo:**
- `Expectativas_dummy`: 1 si expectativas > 50 (optimistas), 0 si ≤50 (pesimistas)

## Transformaciones y Nuevas Variables

### Rezagos (lag1)
- `Tipo_Cambio_Promedio_lag1`
- `IPC_lag1`
- `PBI_Mensual_lag1`
- `Tasa_Referencia_PM_lag1`

### Variaciones Mensuales (Δ)
- `delta_Tipo_Cambio_Promedio`
- `delta_IPC`
- `delta_PBI_Mensual`
- `delta_Tasa_Referencia_PM`

### Interacciones
- `TCxIPC`: Tipo_Cambio_Promedio × IPC
- `TCxTasa`: Tipo_Cambio_Promedio × Tasa_Referencia_PM

### Transformaciones Logarítmicas
- `log_TC`: log(Tipo_Cambio_Promedio)
- `log_PBI`: log(PBI_Mensual)
- `log_IPC`: log(IPC)

## Metodología

### 1. Preprocesamiento
- Conversión de fecha a formato datetime
- Creación de variables derivadas
- Eliminación de valores nulos por rezagos
- Estandarización de características

### 2. Análisis de Componentes Principales (PCA)
- 2 componentes principales explican ~67.4% de la varianza
- PC1: ~53.8% (estabilidad económica vs deterioro)
- PC2: ~13.7% (cambios macroeconómicos recientes)

### 3. Modelos Implementados

#### **Logistic Regression**
- Métricas obtenidas:
  - Precision: 0.75
  - Recall: 0.75
  - F1: 0.75
  - ROC-AUC: 0.79

#### **Random Forest**
- Optimizado con GridSearchCV
- Mejores parámetros: `{'max_depth': 3, 'min_samples_split': 2, 'n_estimators': 200}`
- ROC-AUC: 0.92

#### **XGBoost**
- Optimizado con GridSearchCV
- Mejores parámetros: `{'learning_rate': 0.01, 'max_depth': 3, 'n_estimators': 100}`
- ROC-AUC: 0.91

### 4. Manejo de Costos y Umbral Óptimo
- Costo Falso Positivo: 3
- Costo Falso Negativo: 1
- **Umbral óptimo identificado: 0.33**

## Resultados Clave

### Comparación de Modelos
1. **Random Forest**: Mejor desempeño (AUC = 0.92)
2. **XGBoost**: Alto desempeño (AUC = 0.91)
3. **Logit**: Desempeño razonable (AUC = 0.79)

### Interpretación Económica
- Las expectativas económicas responden a patrones macroeconómicos estructurales
- Existen relaciones no lineales que los modelos avanzados capturan mejor
- El PCA valida la existencia de ciclos económicos visibles
- El umbral conservador (0.33) refleja preferencia por prudencia económica

## Estructura del Notebook

1. **Introducción y Configuración**
2. **Carga y Preprocesamiento de Datos**
3. **Ingeniería de Características**
4. **Análisis PCA**
5. **Modelado con Logit**
6. **Optimización de Random Forest y XGBoost**
7. **Comparación de Modelos**
8. **Análisis de Costos y Umbral Óptimo**

## Requisitos

### Librerías Principales
```python
pandas, numpy, matplotlib, seaborn
scikit-learn, xgboost, imbalanced-learn
```

### Instalación
```bash
pip install xgboost imbalanced-learn
```

## Conclusiones

- Los modelos de ensemble (Random Forest y XGBoost) superan significativamente al modelo lineal
- La estructura económica peruana presenta patrones no lineales complejos
- El análisis de costos permite decisiones más realistas en contexto económico
- El modelo final proporciona una herramienta robusta para predecir expectativas económicas

## Archivos del Proyecto

- `TRABAJO_3.ipynb`: Notebook principal con análisis completo
- `dataset_bcrp_limpio.csv`: Dataset utilizado
- `README.md`: Este documento

---

**Grupo 1:**
- Abad Aniceto Anguiela Brilletth
- Meyli Yanely Robledo Jimenez
- Alberto Sebastian Pizarro Otero
- Damaris Belen Navarro Lozada

**Curso:** Introducción a Ciencia de Datos y Machine Learning con Python
