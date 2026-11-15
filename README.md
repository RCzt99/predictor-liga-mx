# ⚽ Predictor Liga MX — Duelo de Modelos (v1 vs v2 vs v3)

[![Open in Kaggle](https://img.shields.io/badge/Kaggle-Ver_Notebook-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)](https://www.kaggle.com/code/gerardocruzm/predictor-liga-mx-v1-vs-v2)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)

Sistema de predicción probabilística **1X2 (Local / Empate / Visita)** y de **goles esperados (xG)** para la **Liga MX**, combinando modelos estadísticos de fútbol (**Elo dinámico + Dixon-Coles Poisson**) con algoritmos de **Machine Learning** entrenados sin *data leakage* sobre datos históricos reales.

---

## 🧠 Evolución de los motores

| Versión | Arquitectura | Características clave |
| :--- | :--- | :--- |
| **v1 — Original** | Dixon-Coles + `HistGradientBoosting` (55% / 45%) | Elo base (+60 localía), fuerza de ataque/defensa, forma últimos 5 partidos, diferencia de altitud y días de descanso. |
| **v2 — Calibrada** | `LogisticRegression` (50%) + `HGB` (40%) + `DC` (10%) | Elimina doble conteo de localía, añade choque de altitud (`>=2000m` vs `<=800m`), regresión a la media y reinicio parcial entre torneos cortos (`>25 días`). |
| **v3 — Split + EMA + Opt** | Ensamble optimizado (`SLSQP`) sobre ventana cronológica | Fuerza **separada Casa/Visita** (60% global + 40% localía), ritmo goleador de liga por **EMA**, tendencia al empate, historial directo (*H2H*) y matriz de marcadores calibrada. |

---

## 📊 Evaluación histórica (Últimos 300 partidos reales)

> Métricas estrictamente *out-of-sample* (menor = mejor).

| Modelo | Log-Loss | Brier Score |
| :--- | :---: | :---: |
| **v1 (Original)** | `1.0604` | `0.6389` |
| **v2 (Calibrada)** | `1.0530` | `0.6349` |
| **v3 (Split + EMA)** | `ACTUALIZAR_AQUÍ` | `ACTUALIZAR_AQUÍ` |

---

## 📄 Hoja de calificación auto-actualizable (PDF)

El notebook genera automáticamente **`predicciones_ligamx_v1_v2_v3.pdf`** en formato A4 horizontal con:
- Fecha, Elo actual de cada club y probabilidades **1X2** de **v1 vs v2 vs v3**.
- **xG** y **Marcador más probable** calibrado con `v3`.
- **Auto-calificación en vivo:** al volver a ejecutar el notebook cuando se actualiza el CSV oficial, rellena los marcadores reales (entrenando solo con datos previos a la jornada) y marca los aciertos (`OK` / `X`) de cada versión.

---

## 🛠️ Fuente de datos y ejecución

- **Datos:** Descarga automática de resultados históricos de Liga MX desde [`football-data.co.uk`](https://www.football-data.co.uk/new/MEX.csv).
- **Cómo correrlo:**
  1. Abre el notebook directamente en [Kaggle](https://www.kaggle.com/code/gerardocruzm/predictor-liga-mx-v1-vs-v2) y presiona **Run All**, o
  2. Clona el repositorio e instala dependencias:
     ```bash
     pip install -r requirements.txt
     ```

---

## ⚠️ Aviso
Proyecto con fines educativos, estadísticos y de análisis deportivo. No constituye asesoría ni recomendación de apuestas.
