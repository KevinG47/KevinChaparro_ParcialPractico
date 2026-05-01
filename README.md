# Detección de Fraude Bancario — Parcial Práctico ML 2026-I

![Python](https://img.shields.io/badge/Python-3.11-blue)
![PySpark](https://img.shields.io/badge/PySpark-3.5.0-orange)
![LightGBM](https://img.shields.io/badge/LightGBM-4.3.0-green)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED)

**Estudiante:** Kevin Leonardo Chaparro Reyes  
**Semilla:** `2948`  
**Modelo asignado:** LightGBM (scikit-learn)  
**Curso:** Machine Learning con PySpark y Docker — 2026-I  

---

## Sobre el proyecto

Un banco europeo necesita detectar transacciones fraudulentas de forma automática. El reto principal es que los fraudes son extremadamente raros: apenas el 0.17% del dataset (344 de 199,364 transacciones). Se entrenaron 3 modelos distintos y se seleccionó el que mejor equilibra la detección de fraudes reales con la minimización de falsas alarmas.

---

## Estructura del repositorio
KevinChaparro_ParcialPractico/
├── notebooks/
│   └── parcial_Kevin.ipynb
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
├── datos/                        ← no incluido (ver instrucciones)
│   ├── train.csv
│   ├── test.csv
│   └── sample_submission.csv
├── submission.csv
├── reporte_parcial_ML.pdf
└── README.md
---

## Cómo ejecutarlo

**Requisitos:** Docker Desktop y Git instalados.

**1.** Clonar el repositorio:
```bash
git clone https://github.com/KevinG47/KevinChaparro_ParcialPractico.git
cd KevinChaparro_ParcialPractico
```

**2.** Colocar los archivos de datos (`train.csv`, `test.csv`, `sample_submission.csv`) dentro de la carpeta `datos/`.

**3.** Levantar el contenedor:
```bash
cd docker
docker-compose up -d --build
```

**4.** Abrir Jupyter en el navegador: [http://localhost:8888](http://localhost:8888) — Token: `ml2026`

**5.** Abrir `notebooks/parcial_Kevin.ipynb` y ejecutar Kernel → Restart & Run All.

---

## Resultados

Se compararon 3 modelos, todos entrenados con SMOTE para manejar el desbalanceo extremo y con threshold tuning para optimizar el umbral de decisión:

| Modelo | Framework | F1 (fraude) | AUC-ROC | Umbral |
|--------|-----------|-------------|---------|--------|
| Logistic Regression | PySpark MLlib | 0.7451 | 0.9847 | 0.88 |
| Gradient Boosted Trees | PySpark MLlib | 0.8028 | 0.9674 | 0.89 |
| **LightGBM (seleccionado)** | scikit-learn | **0.8992** | **0.9858** | **0.83** |

El modelo final genera solo 2 falsas alarmas y detecta el 84% de los fraudes reales.

---

## Qué técnicas se usaron

- **SMOTE** para balancear las clases (de 275 fraudes a 159,216 por clase)
- **GridSearch** evaluando 64 combinaciones de hiperparámetros
- **Threshold tuning** para encontrar el umbral óptimo de cada modelo
- **Regularización L1/L2** para evitar sobreajuste sobre datos sintéticos
- **train_test_split con stratify** para un split determinista y reproducible

---

## Datos del parcial

- **Semilla:** 2948
- **Train:** 159,491 filas — 275 fraudes
- **Validation:** 39,873 filas — 69 fraudes
- **F1 modelo final:** 0.8992
- **Fraudes predichos en test:** 69

---

## Tecnologías

- Python 3.11
- PySpark 3.5.0
- LightGBM 4.3.0
- scikit-learn 1.4.0
- imbalanced-learn 0.12.0
- Docker + Jupyter Lab