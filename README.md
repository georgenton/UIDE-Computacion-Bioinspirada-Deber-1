# 🧬 Computación Bioinspirada — Tarea 2
### Algoritmos Genéticos y Modelos de Computación Evolutiva

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
| **Grupo** | Grupo 3 |
| **Integrantes** | César Nelson Abarca Araujo · Jorge Armando Quizamanchuro Fuel · Robinson Damián Chiluisa Gallardo |
| **Fecha** | Abril 2026 |

---

## 🎯 Objetivo del Reto

Adaptar un **Algoritmo Genético con Fitness Sharing** a una nueva función objetivo multimodal más compleja y analizar críticamente el impacto del parámetro **`SIGMA_SHARE`** en su capacidad para identificar múltiples óptimos simultáneamente.

---

## 📁 Estructura del Repositorio

```
UIDE-Computacion-Bioinspirada-Deber-2/
│
├── tarea2_AG_bioinspirada_FINAL.ipynb   # Notebook principal (entregable)
└── README.md                            # Este archivo
```

---

## 📚 Contenido del Notebook

### Contexto Teórico — Fitness Sharing y Niching

Un AG estándar converge prematuramente al único óptimo global, descartando todos los picos secundarios. El **Fitness Sharing** soluciona esto penalizando a los individuos que compiten dentro del mismo nicho, permitiendo que múltiples subpoblaciones coexistan en distintos picos simultáneamente.

**Fórmulas clave:**

| Concepto | Fórmula |
|---|---|
| Función de compartición | `sh(d) = 1 - (d/σ)^α` si `d < σ`, `0` si no |
| Conteo de nicho | `m_i = Σ sh(d_ij)` para todos los j |
| Fitness compartido | `f'_i = f_i / m_i` |

---

### PARTE 1 — Nueva Función Objetivo (4 Picos)

Se diseña una función multimodal con **4 picos gaussianos**, donde 2 de ellos están intencionalmente cerca:

| Pico | Posición (x) | Altura | Característica |
|---|---|---|---|
| 1 | 1.5 | ≈ 1.00 | Pico más alto |
| 2 | 2.5 | ≈ 0.85 | **Cercano al Pico 1** (distancia = 1.0) |
| 3 | 5.5 | ≈ 0.95 | Pico intermedio |
| 4 | 8.5 | ≈ 0.90 | Pico lejano |

Los picos 1 y 2 están separados solo **1.0 unidad**, lo que los hace difíciles de distinguir con valores de `SIGMA_SHARE` demasiado grandes.

---

### PARTE 2 — Experimentación con SIGMA_SHARE

Se ejecuta el AG tres veces, variando únicamente `SIGMA_SHARE`:

| Experimento | SIGMA_SHARE | Relación con distancia entre picos cercanos (1.0) | Picos detectados |
|---|---|---|---|
| 1 | **2.0** | Significativamente **MAYOR** | ~2/4 — fusiona picos cercanos |
| 2 | **0.8** | Aproximadamente **IGUAL/MENOR** ✅ | 4/4 — balance óptimo |
| 3 | **0.3** | Significativamente **MENOR** | Varía — nichos diminutos |

Cada experimento genera:
- Gráfico de la función objetivo con la distribución de la población final
- Gráfico de convergencia del fitness por generación

---

### PARTE 3 — Análisis del Impacto de SIGMA_SHARE

- Explicación detallada de cada experimento con analogías
- **Gráfico de sensibilidad** con 12 valores de SIGMA_SHARE (0.1 a 3.0)
- Conclusión: el valor adecuado es aproximadamente `0.6–0.9 × distancia_mínima_entre_picos`

**Regla práctica:** `SIGMA_SHARE_adecuado ≈ 0.8 × distancia_mínima_entre_picos`

---

### PARTE 4 — Planteamientos en Entorno Laboral

Cada miembro del grupo plantea un problema real de su área de expertise aplicable con Algoritmos Genéticos, incluyendo función objetivo y estructura del cromosoma.

---

#### 👤 César Nelson Abarca Araujo
**Optimización de Configuración de Infraestructura de Red Corporativa**

> Encontrar la configuración óptima de ancho de banda, QoS, switches, VLANs y protocolos de una red corporativa, maximizando rendimiento y redundancia mientras se minimiza el costo operativo.

**Función objetivo:**
```
f(x) = 0.4·Throughput - 0.3·Latencia - 0.2·Costo + 0.1·Redundancia
```

**Cromosoma — 8 genes:**

| Gen | Característica | Tipo | Rango |
|---|---|---|---|
| G1 | Ancho de banda oficinas (Mbps) | Entero | 100, 200, 500, 1000 |
| G2 | Ancho de banda servidores (Mbps) | Entero | 1000, 2500, 5000, 10000 |
| G3 | Prioridad QoS VoIP | Entero | 1–5 |
| G4 | Switches de distribución activos | Entero | 2, 4, 6, 8 |
| G5 | Tipo de enlace WAN | Categórico | MPLS / SD-WAN / Fibra |
| G6 | Redundancia de enlace | Binario | 0=Sin / 1=Con |
| G7 | Segmentación VLAN | Entero | 4, 8, 16, 32 |
| G8 | Protocolo de enrutamiento | Categórico | OSPF / BGP / EIGRP |

**Genotipo ejemplo:** `[500, 5000, 4, 4, 'SD-WAN', 'Con', 16, 'OSPF']`

**Fenotipo:** *"500 Mbps oficinas, 5 Gbps servidores, QoS nivel 4, 4 switches activos, SD-WAN con redundancia activa, 16 VLANs, protocolo OSPF"*

**Por qué multimodal:** Cada sede corporativa (Quito, Guayaquil, Cuenca) tiene su configuración óptima diferente → el Fitness Sharing permite encontrar la configuración óptima para **cada sede simultáneamente**.

---

#### 👤 Jorge Armando Quizamanchuro Fuel
**Optimización de Arquitectura y Configuración de Plataforma SaaS Multi-Tenant**

> En el desarrollo de una plataforma SaaS multi-tenant con NestJS + Nx Monorepo, determinar la configuración óptima de microservicios (réplicas, memoria, estrategia de DB, caché, autoescalado) para maximizar rendimiento y escalabilidad minimizando costo y latencia.

**Función objetivo:**
```
f(x) = 0.35·Rendimiento + 0.30·Escalabilidad - 0.20·Costo - 0.15·Latencia_p95
Penalización: -1000 si latencia_p95 > 200ms | -300 si costo > presupuesto
```

**Cromosoma — 10 genes:**

| Gen | Característica | Tipo | Rango |
|---|---|---|---|
| G1 | Réplicas del servicio NestJS | Entero | 1, 2, 4, 8 |
| G2 | Límite RAM por pod (MB) | Entero | 256, 512, 1024, 2048 |
| G3 | Aislamiento de DB por tenant | Categórico | Schema / DB-per / Row-level |
| G4 | Proveedor de caché distribuida | Categórico | Redis / Memcached / Sin caché |
| G5 | TTL de caché (segundos) | Entero | 60, 300, 900, 3600 |
| G6 | Estrategia de autoescalado | Categórico | HPA-CPU / HPA-RAM / KEDA |
| G7 | Tipo de balanceador de carga | Categórico | Round-Robin / Least-Conn / IP-Hash |
| G8 | Workers del proceso Node.js | Entero | 1, 2, 4, 8 |
| G9 | Connection pooling Prisma | Binario | 0=Deshabilitado / 1=Habilitado |
| G10 | Tamaño del pool de conexiones DB | Entero | 5, 10, 20, 50 |

**Genotipo ejemplo:** `[4, 1024, 'Schema', 'Redis', 300, 'KEDA', 'Least-Conn', 4, 1, 20]`

**Fenotipo:** *"4 réplicas NestJS con 1GB RAM, aislamiento Schema-per-tenant, Redis TTL=5min, autoescalado KEDA por eventos, balanceo Least-Connections, 4 workers Node.js, Prisma connection pool de 20 conexiones"*

**Por qué multimodal:** Tenants con uso intensivo de base de datos necesitan una configuración diferente a los que tienen uso intensivo de API → el Fitness Sharing mantiene subpoblaciones óptimas para **cada perfil de tenant** simultáneamente.

---

#### 👤 Robinson Damián Chiluisa Gallardo
**Optimización de Diseño Aerodinámico de Superficies mediante Computación Evolutiva**

> Encontrar la geometría óptima de perfiles aerodinámicos (alas, palas de turbina, carrocerías) que maximice la eficiencia aerodinámica CL/CD minimizando la resistencia al avance y maximizando la sustentación.

**Función objetivo:**
```
f(x) = 0.3·(CL/CL_max) - 0.4·(CD/CD_max) + 0.3·(CL/CD / eficiencia_max)
Penalización: -800 si espesor < umbral mínimo | -1000 si desprendimiento de capa límite
```

**Cromosoma — 8 genes reales continuos:**

| Gen | Característica geométrica | Tipo | Rango |
|---|---|---|---|
| G1 | Curvatura máxima — camber (% cuerda) | Real | 0.0% – 9.0% |
| G2 | Posición de curvatura máxima (% cuerda) | Real | 10% – 90% |
| G3 | Espesor máximo (% cuerda) | Real | 6% – 24% |
| G4 | Ángulo de ataque (grados) | Real | -5° – 20° |
| G5 | Radio del borde de ataque (% cuerda) | Real | 0.5% – 5.0% |
| G6 | Ángulo del borde de salida (grados) | Real | 0° – 15° |
| G7 | Relación de aspecto (envergadura/cuerda) | Real | 4.0 – 12.0 |
| G8 | Número de Mach de diseño | Real | 0.1 – 0.85 |

**Genotipo ejemplo:** `[2.4, 40.0, 12.0, 5.0, 1.6, 6.0, 8.0, 0.3]`

**Fenotipo:** *"Perfil alar: camber 2.4% a 40% de la cuerda, espesor 12%, ángulo de ataque 5°, radio de ataque 1.6%, borde de salida 6°, relación de aspecto 8:1, diseñado para Mach 0.3"*

**Por qué multimodal:** Un perfil óptimo para baja velocidad (planeador) es geométricamente diferente al óptimo para alta velocidad (jet) → el Fitness Sharing permite mantener **subpoblaciones de diseños óptimos para cada régimen de vuelo** sin que uno elimine al otro.

---

### Comparativa de Cromosomas

| Miembro | Tipo de genes | N° genes | Codificación | Espacio de búsqueda |
|---|---|---|---|---|
| César Abarca | Mixto | 8 | Entero + Categórico | ~3×10⁴ combinaciones |
| Jorge Quizamanchuro | Mixto | 10 | Entero + Categórico | ~5×10⁵ combinaciones |
| Robinson Chiluisa | Real continuo | 8 | Valores reales ℝ | Infinito (espacio ℝ⁸) |

---

## 🛠️ Instalación y Ejecución

### Requisitos
- Python 3.8 o superior
- pip3

### Instalar dependencias

```bash
pip3 install numpy matplotlib jupyter
```

### Ejecutar el notebook

```bash
# Opción 1: Jupyter en el navegador
jupyter notebook tarea2_AG_bioinspirada_FINAL.ipynb

# Opción 2: Directamente en VS Code
code tarea2_AG_bioinspirada_FINAL.ipynb
```

---

## 📊 Parámetros del Algoritmo Genético

| Parámetro | Valor | Descripción |
|---|---|---|
| `POPULATION_SIZE` | 100 | Número de individuos |
| `NUM_GENERATIONS` | 150 | Iteraciones del ciclo evolutivo |
| `MUTATION_RATE` | 0.1 | Probabilidad de mutación |
| `MUTATION_STRENGTH` | 0.4 | Desviación estándar de la mutación gaussiana |
| `TOURNAMENT_SIZE` | 3 | Individuos por torneo de selección |
| `CROSSOVER_RATE` | 0.8 | Probabilidad de cruce aritmético |
| `ALPHA_SHARING` | 1.0 | Exponente de la función de compartición (lineal) |
| `SIGMA_SHARE` | 2.0 / 0.8 / 0.3 | Radio del nicho — variable experimental |

---

## 🧬 Conceptos Aplicados

```
Algoritmo Genético con Fitness Sharing
├── Génesis (población inicial aleatoria)
├── Evaluación
│   ├── Fitness original: f(x) — calidad real de la solución
│   └── Fitness compartido: f'(x) = f(x) / niche_count
│       └── sh(d) = 1 - (d/σ)^α  si d < σ  →  penaliza nichos densos
├── Selección por torneo (usa fitness COMPARTIDO)
├── Cruce aritmético: child = α·p1 + (1-α)·p2
├── Mutación gaussiana: x += N(0, σ_mutación)
└── Nueva generación → repetir hasta convergencia

Resultado: múltiples subpoblaciones estables en distintos picos
```

---

## 📖 Referencias

- Holland, J.H. (1975). *Adaptation in Natural and Artificial Systems*. MIT Press.
- Goldberg, D.E., & Richardson, J. (1987). *Genetic algorithms with sharing for multimodal function optimization*. ICGA.
- Kennedy, J., & Eberhart, R. (1995). *Particle swarm optimization*. ICNN.
- Deb, K. (2001). *Multi-Objective Optimization Using Evolutionary Algorithms*. Wiley.

---

## 📄 Licencia

Este proyecto es de uso académico para la Maestría en Inteligencia Artificial Aplicada — UIDE.