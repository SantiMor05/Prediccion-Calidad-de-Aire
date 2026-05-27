# 🌫️ Predicción de la concentración de PM2.5 en Lima Metropolitana

> Tarea Académica — Inteligencia Artificial (1INF24) | PUCP 2026-1

---

## 📋 Descripción

Este proyecto aplica modelos de regresión supervisada para predecir la concentración horaria de **PM2.5** (material particulado fino, µg/m³) en las 7 estaciones de monitoreo de Lima Metropolitana, utilizando datos históricos del SENAMHI (2015–2024).

El PM2.5 es el contaminante atmosférico con mayor impacto documentado en la salud pública. En Lima, el **69.3%** de las mediciones horarias registradas superan el límite guía de la OMS (15 µg/m³), lo que hace de su predicción una herramienta de alto valor para alertas tempranas y gestión ambiental urbana.

---

## 🎯 Objetivo

Comparar el desempeño predictivo de tres modelos de regresión:

| Modelo | Tipo |
|---|---|
| Regresión Lineal Múltiple | Lineal (baseline) |
| Árbol de Regresión | No lineal |
| K-Nearest Neighbors (KNN) | No lineal |

**Hipótesis:** Los modelos no lineales (árbol de regresión y KNN) superan a la regresión lineal múltiple al capturar mejor las relaciones complejas entre contaminantes y variables temporales/espaciales.

---

## 📂 Estructura del repositorio

```
├── data/
│   └── senamhi_aire_lima.csv        # Dataset original del SENAMHI
├── notebooks/
│   ├── 01_exploracion.ipynb         # Análisis exploratorio del dataset
│   ├── 02_preprocesamiento.ipynb    # Limpieza y transformación de datos
│   └── 03_modelos.ipynb             # Entrenamiento y comparación de modelos
├── src/
│   ├── preprocessing.py             # Funciones de preprocesamiento
│   └── models.py                    # Implementación de los 3 modelos
├── results/
│   └── metricas.csv                 # Resultados MAE, RMSE, R² por modelo
├── informe/
│   └── GRUPO3-TA-Parcial.pdf        # Informe parcial entregado
└── README.md
```

---

## 📊 Dataset

- **Fuente:** SENAMHI — Plataforma Nacional de Datos Abiertos del Perú
- **Link:** https://www.datosabiertos.gob.pe/dataset/monitoreo-de-los-contaminantes-del-aire-en-lima-metropolitana-servicio-nacional-de
- **Período:** Enero 2015 – Mayo 2024
- **Estaciones:** San Borja, Campo de Marte, Santa Anita, Villa María del Triunfo, San Juan de Lurigancho, San Martín de Porres, Carabayllo

### Variables utilizadas

| Variable | Tipo | Descripción |
|---|---|---|
| `PM2_5` | Float | **Target** — Concentración de PM2.5 (µg/m³) |
| `PM10` | Float | Concentración de PM10 (µg/m³) |
| `NO2` | Float | Concentración de NO2 (µg/m³) |
| `hora` | Integer | Hora del registro (0–23) |
| `mes` | Integer | Mes del registro (1–12) |
| `anio` | Integer | Año del registro (2015–2024) |
| `ALTITUD` | Float | Altitud de la estación (m.s.n.m.) |
| `ESTACION` | Categórica | Estación de monitoreo (one-hot encoding) |

---

## ⚙️ Metodología

### Preprocesamiento
1. Filtrado de registros con PM2.5 válido
2. Imputación por mediana para valores faltantes en PM10 y NO2
3. Extracción de variables temporales (hora, mes, año) desde campos FECHA y HORA
4. One-hot encoding para la variable ESTACION
5. Estandarización de variables numéricas (media 0, desviación estándar 1) para KNN y Regresión Lineal

### Modelos

**Regresión Lineal Múltiple (baseline)**
```
ŷ = β₀ + β₁·PM10 + β₂·NO2 + β₃·hora + β₄·mes + β₅·año + β₆·altitud + Σβₖ·estación_k
```

**Árbol de Regresión**
- Hiperparámetros ajustados via Grid Search + 5-fold CV
- `max_depth` ∈ {3, 5, 7, 10, 15}
- `min_samples_split` ∈ {2, 10, 50}
- `min_samples_leaf` ∈ {1, 5, 20}

**KNN Regressor**
- Distancia euclidiana sobre variables estandarizadas
- `k` ∈ {3, 5, 7, 10, 15, 20}
- `weights` ∈ {uniform, distance}

### Validación
- División: 60% entrenamiento / 20% validación / 20% prueba
- Estratificación por estación de monitoreo
- Métricas: **MAE**, **RMSE**, **R²**

---


## 📚 Referencias

1. Zamani Joharestani, M., et al. (2019). PM2.5 prediction based on random forest, XGBoost, and deep learning using multisource remote sensing data. *Atmosphere*, 10(7), 373. https://doi.org/10.3390/atmos10070373

2. Rybarczyk, Y., & Zalakeviciute, R. (2018). Machine learning approaches for outdoor air quality modelling: A systematic review. *Applied Sciences*, 8(12), 2570. https://doi.org/10.3390/app8122570

3. Suleiman, A., et al. (2019). Applying machine learning methods in managing urban concentrations of traffic-related particulate matter (PM10 and PM2.5). *Atmospheric Pollution Research*, 10(1), 134–144. https://doi.org/10.1016/j.apr.2018.07.001

4. SENAMHI. (2024). Monitoreo de los contaminantes del aire en Lima Metropolitana. Plataforma Nacional de Datos Abiertos del Perú. https://www.datosabiertos.gob.pe/dataset/monitoreo-de-los-contaminantes-del-aire-en-lima-metropolitana-servicio-nacional-de

---

## 👥 Autores

| Nombre | Código |
|---|---|
| Esteban Leonardo Guevara Sanchez | 20231348 |
| Diego Gharnerd Ayala de la Cruz | 20233483 |
| Matias Jesús Iturri Mendoza | 20230827 |
| Álvaro Francisco Armas Jáuregui | 20231067 |
| Santiago Mijael Alexandre Moreno Galvez | 20231523 |

---

> Curso: Inteligencia Artificial (1INF24) — Facultad de Ciencias e Ingeniería — PUCP 2026-1
