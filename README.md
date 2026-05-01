# 🏦 Detección de Fraude Bancario — Parcial Práctico ML 2026-I

![Python](https://img.shields.io/badge/Python-3.11-blue)
![PySpark](https://img.shields.io/badge/PySpark-3.5.0-orange)
![LightGBM](https://img.shields.io/badge/LightGBM-4.3.0-green)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED)
![Universidad](https://img.shields.io/badge/Universidad-Santo%20Tomás-red)

**Estudiante:** Kevin Leonardo Chaparro Reyes  
**Semilla personal:** `2948`  
**Modelo asignado:** LightGBM (scikit-learn)  
**Curso:** Machine Learning con PySpark y Docker — 2026-I  

---

## 📋 Descripción del Problema

Una entidad bancaria europea registra millones de transacciones diarias. El dataset presenta un desbalanceo extremo: solo el **0.173% de las transacciones son fraudulentas** (344 de 199,364). El objetivo es construir un sistema automatizado que detecte fraudes minimizando los falsos negativos sin generar demasiadas falsas alarmas.

---

## 📁 Estructura del Repositorio

KevinChaparro_ParcialPractico/
├── notebooks/
│   └── parcial_Kevin.ipynb       ← Notebook principal
├── docker/
│   ├── Dockerfile                ← Imagen con todas las dependencias
│   └── docker-compose.yml        ← Configuración del entorno
├── datos/                        ← NO incluido en el repo (ver instrucciones)
│   ├── train.csv
│   ├── test.csv
│   └── sample_submission.csv
├── submission.csv                ← Predicciones del mejor modelo
├── reporte.pdf                   ← Reporte de 1 página
└── README.md
---

## 🐳 Instrucciones para Ejecutar

### Prerrequisitos
- Docker Desktop instalado y corriendo
- Git instalado

### Pasos

**1. Clonar el repositorio**
```bash
git clone https://github.com/KevinG47/KevinChaparro_ParcialPractico.git
cd KevinChaparro_ParcialPractico
```

**2. Agregar los datos**  
Copia los archivos `train.csv`, `test.csv` y `sample_submission.csv` dentro de la carpeta `datos/`.

**3. Levantar el contenedor**
```bash
cd docker
docker-compose up -d --build
```

**4. Abrir Jupyter Lab**  
Abre tu navegador en: [http://localhost:8888](http://localhost:8888)  
Token: `ml2026`

**5. Ejecutar el notebook**  
Abre `notebooks/parcial_Kevin.ipynb` y ejecuta **Kernel → Restart & Run All**

---

## 🤖 Modelos Implementados

| # | Modelo | Framework | F1 (clase fraude) | AUC-ROC |
|---|--------|-----------|-------------------|---------|
| 1 | Logistic Regression | PySpark MLlib | 0.2351 | 0.9909 |
| 2 | Gradient Boosted Trees | PySpark MLlib | 0.3158 | 0.9865 |
| 3 | **LightGBM + SMOTE** ⭐ | scikit-learn | **0.8769** | **0.9855** |

> ⭐ Modelo seleccionado para submission

---

## 🔑 Técnicas Clave

- **SMOTE** — Balanceo de clases generando fraudes sintéticos (275 → 159,216)
- **Threshold tuning** — Umbral óptimo de 0.76 en lugar del default 0.5
- **Regularización L1/L2** — `reg_alpha=0.1`, `reg_lambda=0.1`
- **train_test_split con stratify** — Split determinista y proporcional

---

## 📊 Resultados Finales

- **Semilla:** 2948  
- **Train:** 159,491 filas | 275 fraudes  
- **Validation:** 39,873 filas | 69 fraudes  
- **F1 modelo final (LightGBM):** `0.8769`  
- **Fraudes predichos en test:** 72  

---

## 🛠️ Stack Tecnológico

- Python 3.11
- PySpark 3.5.0
- LightGBM 4.3.0
- scikit-learn 1.4.0
- imbalanced-learn 0.12.0
- Docker + Jupyter Lab
