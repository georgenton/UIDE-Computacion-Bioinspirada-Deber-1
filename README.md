# 🧠 Computación Bioinspirada — Tarea 1
### Lógica Difusa y Algoritmos de Adaptación Social
 
![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green)
 
---
 
## 📋 Información del Proyecto
 
| Campo | Detalle |
|---|---|
| **Materia** | Computación Bioinspirada |
| **Programa** | Maestría en Inteligencia Artificial Aplicada (MIA-B) |
| **Universidad** | UIDE — Universidad Internacional del Ecuador |
| **Docente** | Marcelo Guato Burgos, PhD |
| **Alumno** | Jorge Quizamacho |
| **Fecha** | Abril 2026 |
 
---
 
## 🎯 Objetivo
 
Aplicar conocimientos teóricos de **Lógica Difusa** y **algoritmos de adaptación social** en implementaciones informáticas mediante Python, desarrollando sistemas de control inteligente capaces de operar en entornos de incertidumbre.
 
---
 
## 📁 Estructura del Repositorio
 
```
UIDE-Computacion-Bioinspirada-Deber-1/
│
├── tarea_bioinspirada_FINAL.ipynb   # Notebook principal (entregable)
└── README.md                        # Este archivo
```
 
---
 
## 📚 Contenido del Notebook
 
### PARTE 1 — Lógica Difusa (50%)
 
#### 🚗 Problema 1: Control de Derrape Vehicular
 
Sistema de control difuso que determina la respuesta óptima del conductor ante una situación de derrape, considerando:
 
**Caso A — Tracción Delantera**
| Elemento | Detalle |
|---|---|
| **Antecedentes** | Ángulo de derrape (0°–45°), Velocidad (0–120 km/h), Humedad calzada (0–100%) |
| **Consecuentes** | Corrección del volante (0°–45°), Intensidad de frenado (0–100%) |
| **Funciones de pertenencia** | Triangular (`trimf`) y Trapezoidal (`trapmf`) |
| **Reglas difusas** | 12 reglas IF-THEN |
 
**Caso B — Tracción Trasera**
| Elemento | Detalle |
|---|---|
| **Antecedentes** | Ángulo de derrape (0°–45°), % Acelerador pisado (0–100%), Humedad calzada (0–100%) |
| **Consecuentes** | Corrección del volante (0°–45°), Reducción del acelerador (0–100%) |
| **Funciones de pertenencia** | Triangular (`trimf`) y Trapezoidal (`trapmf`) |
| **Reglas difusas** | 12 reglas IF-THEN |
 
> **Diferencia clave:** En tracción trasera la acción principal es soltar el acelerador, no frenar. En tracción delantera es la corrección del volante con frenado muy suave.
 
---
 
#### 💳 Problema 2: Evaluación de Riesgo Crediticio *(Aplicación en entorno laboral)*
 
Sistema difuso para el sector financiero/bancario que evalúa el riesgo de un solicitante de crédito combinando variables inherentemente difusas:
 
| Elemento | Detalle |
|---|---|
| **Antecedentes** | Ingreso mensual neto (0–$10.000), Nivel de endeudamiento (0–100%), Score de historial crediticio (0–100 pts) |
| **Consecuente** | Nivel de riesgo crediticio (0–100) |
| **Decisión** | ✅ Aprobado / ⚠️ Condicional / ❌ Rechazado |
 
---
 
### PARTE 2 — PSO: Formación de Drones (50%)
 
Implementación del algoritmo **PSO (Particle Swarm Optimization)** para optimizar las posiciones de una flota de 6 drones manteniendo formaciones geométricas dentro de un área de vuelo de 100×100 metros.
 
#### Parámetros del algoritmo
 
| Parámetro | Valor | Descripción |
|---|---|---|
| `NUM_DRONES` | 6 | Drones en la flota |
| `NUM_PARTICLES` | 80 | Tamaño del enjambre |
| `MAX_ITERATIONS` | 200 | Iteraciones máximas |
| `W` | 0.5 | Inercia |
| `C1` | 1.5 | Coeficiente cognitivo (pBest) |
| `C2` | 1.5 | Coeficiente social (gBest) |
| `V_MAX` | 10.0 | Velocidad máxima (m/iter) |
| `MIN_SAFE_DISTANCE` | 5.0 m | Distancia mínima entre drones |
 
#### Formaciones implementadas
 
| Formación | Descripción | Estado |
|---|---|---|
| 🟦 **Line** | Fila horizontal de 6 drones | ✅ Código base |
| 🔺 **Triangle** | Pirámide 1-2-3 (6 drones) | ✅ Código base adaptado |
| 🅷 **H** | Dos columnas + barra central | ✅ Implementación adicional |
| 🟥 **Rectangle** | Dos filas paralelas de 3 | ✅ Implementación adicional |
 
#### Función de Fitness
 
```
fitness = w1 × error_formación + w2 × penalización_colisión + w3 × penalización_límites
        =  1.0 × e_form        +  1.0 × p_coll              +  0.5 × p_boundary
```
 
---
 
## 🛠️ Instalación y Ejecución
 
### Requisitos
- Python 3.8 o superior
- pip3
### Instalar dependencias
 
```bash
pip3 install scipy scikit-fuzzy numpy matplotlib networkx jupyter
```
 
### Ejecutar el notebook
 
```bash
# Opción 1: Jupyter en el navegador
jupyter notebook tarea_bioinspirada_FINAL.ipynb
 
# Opción 2: Abrir directamente en VS Code
code tarea_bioinspirada_FINAL.ipynb
```
 
### Primera celda a ejecutar
 
Si es la primera vez, ejecuta primero la celda de instalación automática de dependencias que está al inicio del notebook.
 
---
 
## 📊 Resultados Principales
 
### Lógica Difusa — Escenario representativo
> Derrape moderado (22°), calzada húmeda (75%)
 
| | Caso A — Tracción Delantera | Caso B — Tracción Trasera |
|---|---|---|
| Corrección volante | ~22° | ~26° |
| Acción secundaria | Frenado ~18% | Reducción acelerador ~75% |
| Interpretación | Freno muy suave + corrección | Suelta el gas completamente |
 
### PSO — Convergencia
Todas las formaciones convergen en menos de 200 iteraciones con **0 colisiones** en la solución final.
 
### Formación más eficiente para vuelo real
La **formación rectangular** es la más eficiente porque:
- Minimiza interferencia aerodinámica entre drones
- Cubre área útil para vigilancia o mapeo
- Mayor estabilidad ante perturbaciones de viento
- Mejor resiliencia ante fallo de un dron
---
 
## 🧬 Conceptos Aplicados
 
```
Lógica Difusa                    PSO
├── Universo del discurso        ├── Inicialización aleatoria
├── Variables lingüísticas       ├── Función de fitness
├── Funciones de pertenencia     ├── pBest (mejor personal)
│   ├── Triangular (trimf)       ├── gBest (mejor global)
│   └── Trapezoidal (trapmf)     ├── Actualización de velocidad
├── Reglas IF-THEN               │   v = W·v + C1·r1·(pBest-x)
├── Motor de inferencia          │       + C2·r2·(gBest-x)
└── Defuzzificación              └── Convergencia
    └── Método centroide
```
 
---
 
## 📖 Referencias
 
- Zadeh, L.A. (1965). *Fuzzy sets*. Information and Control, 8(3), 338–353.
- Kennedy, J., & Eberhart, R. (1995). *Particle swarm optimization*. Proceedings of ICNN'95.
- Manual de Oslo (2018). *Directrices para la recogida y comunicación de información relativa a la innovación*. OCDE/Eurostat.
- scikit-fuzzy Documentation: https://pythonhosted.org/scikit-fuzzy/
---
 
## 📄 Licencia
 
Este proyecto es de uso académico para la Maestría en Inteligencia Artificial Aplicada — UIDE.
