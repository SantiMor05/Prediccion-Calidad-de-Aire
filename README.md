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
| Regresión Lineal Múltiple | Lineal |
| Árbol de Regresión | No lineal |
| K-Nearest Neighbors (KNN) | No lineal |

**Hipótesis:** Los modelos no lineales (árbol de regresión y KNN) superan a la regresión lineal múltiple al capturar mejor las relaciones complejas entre contaminantes y variables temporales/espaciales.

---

## 📊 Dataset

- **Fuente:** SENAMHI — Plataforma Nacional de Datos Abiertos del Perú
- **Link:** https://www.datosabiertos.gob.pe/dataset/monitoreo-de-los-contaminantes-del-aire-en-lima-metropolitana-servicio-nacional-de
- **Período:** Enero 2015 – Mayo 2024
- **Estaciones:** San Borja, Campo de Marte, Santa Anita, Villa María del Triunfo, San Juan de Lurigancho, San Martín de Porres, Carabayllo

### Variables utilizadas

Tras el proceso de selección y transformación de variables, se utilizaron las siguientes características para el entrenamiento de los modelos:

| Variable | Tipo | Descripción |
|---|---|---|
| `PM2_5` | Float | **Variable objetivo** — Concentración de PM2.5 (µg/m³) |
| `PM10` | Float | Concentración de PM10 (µg/m³) |
| `NO2` | Float | Concentración de NO2 (µg/m³) |
| `anio` | Integer | Año de la medición |
| `mes` | Integer | Mes de la medición |
| `turno` | Categórica | Turno horario (mañana, tarde o noche) |
| `ALTITUD` | Float | Altitud de la estación (m.s.n.m.) |
| `ESTACION` | Categórica | Estación de monitoreo (codificada mediante One-Hot Encoding) |

### Variables descartadas

Las siguientes variables fueron eliminadas durante el proceso de selección debido a redundancia o falta de capacidad predictiva:

- `DEPARTAMENTO`
- `PROVINCIA`
- `FECHA_CORTE`
- `UBIGEO`
- `DISTRITO`
- `LATITUD`
- `LONGITUD`

---

## ⚙️ Metodología

### Preprocesamiento y selección de variables

El proceso de preparación de datos incluyó las siguientes etapas:

1. Filtrado de registros con valores válidos de PM2.5.
2. Imputación mediante la mediana para valores faltantes en PM10 y NO2.
3. Tratamiento de valores extremos mediante winsorización de PM2.5 a 250 µg/m³.
4. Extracción de variables temporales a partir de la fecha y hora de medición.
5. Transformación de la variable hora en tres categorías: mañana, tarde y noche.
6. Eliminación de variables redundantes o no informativas.
7. Codificación One-Hot Encoding para la variable ESTACION.
8. Escalamiento de variables numéricas para modelos sensibles a la escala.


### Modelos

| Modelo | Configuración inicial |
|---|---|
| Regresión Lineal | Parámetros por defecto |
| Árbol de Regresión | `random_state=7` |
| KNN | `n_neighbors=5` |

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

- Esteban Leonardo Guevara Sanchez
- Diego Gharnerd Ayala de la Cruz
- Matias Jesús Iturri Mendoza
- Álvaro Francisco Armas Jáuregui
- Santiago Mijael Alexandre Moreno Galvez

---

> Curso: Inteligencia Artificial (1INF24) — Facultad de Ciencias e Ingeniería — PUCP 2026-1
