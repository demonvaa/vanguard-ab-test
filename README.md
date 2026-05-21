# Vanguard A/B Test Analysis 🏦

## Descripción del proyecto
Análisis de un experimento A/B realizado por **Vanguard**, empresa de gestión de inversiones con sede en Estados Unidos, para evaluar si una nueva interfaz de usuario (UI) digital aumenta la tasa de finalización del proceso online de sus clientes.

| | |
|---|---|
| **Período del experimento** | 15/03/2017 – 20/06/2017 |
| **Grupo Control** | UI tradicional de Vanguard |
| **Grupo Test** | Nueva UI con indicaciones contextuales |
| **Proceso** | `start → step_1 → step_2 → step_3 → confirm` |

---

## Estructura del repositorio
```
vanguard-ab-test/
├── Proyecto_2.ipynb                    ← Notebook principal con el análisis completo
├── src/
│   └── funciones.py                    ← Funciones reutilizables
├── df_demo_clean.csv                   ← Datos demográficos limpios
├── df_exp_clean.csv                    ← Asignación Control/Test limpia
├── df_web_clean.csv                    ← Huellas digitales limpias
├── df_final.csv                        ← Dataset final unido
├── df_final_demo.csv                   ← Datos demográficos originales
├── df_final_experiment_clients.csv     ← Asignación Control/Test original
├── df_final_web_data_pt_1.csv          ← Huellas digitales parte 1
├── df_final_web_data_pt_2.csv          ← Huellas digitales parte 2
├── Proyecto_Control_Test.twbx          ← Dashboard Tableau
└── README.md
```

---

## Datasets
| Dataset | Descripción | Filas |
|---|---|---|
| `df_final_demo` | Perfil demográfico de cada cliente | 70.609 |
| `df_final_experiment_clients` | Asignación Control/Test | 70.609 |
| `df_final_web_data_pt_1` | Huellas digitales parte 1 | 343.141 |
| `df_final_web_data_pt_2` | Huellas digitales parte 2 | 412.264 |

### Variables principales
| Variable | Descripción |
|---|---|
| `client_id` | Identificador único del cliente |
| `variation` | Grupo del experimento (Control / Test) |
| `process_step` | Paso del proceso digital |
| `date_time` | Timestamp de cada actividad web |
| `clnt_age` | Edad del cliente |
| `clnt_tenure_yr` | Antigüedad con Vanguard (años) |
| `bal` | Saldo total del cliente |
| `gendr` | Género del cliente |

---

## Metodología

### 1. EDA & Limpieza de datos
- Exploración de los 3 datasets (nulos, duplicados, rangos lógicos)
- Eliminación de nulos y registros inconsistentes (edad < 18, género 'X')
- Conversión de tipos de datos y estandarización de columnas
- Unión de datasets por `client_id`
- Creación de `completion_flag`

### 2. KPIs y Métricas de Rendimiento
| KPI | Fórmula |
|---|---|
| **Completion Rate** | clientes en `confirm` / clientes en `start` |
| **Drop-off por paso** | `1 - (N_paso_i+1 / N_paso_i)` |
| **Tiempo por paso** | Diferencia de timestamps entre pasos |
| **Error Rate (Backtracking)** | % visitas con retroceso de pasos |

### 3. Pruebas de Hipótesis
| Hipótesis | Test | Resultado |
|---|---|---|
| H1: CR Test > CR Control | z-test proporciones | ✅ Se rechaza H0 |
| H2: CR supera umbral +5% | t-test una muestra | ❌ No se rechaza H0 |
| H3: Tiempo diferente entre grupos | t-test Welch | ✅ Se rechaza H0 |
| H4: Edad diferente entre grupos | t-test Welch | ✅ Se rechaza H0 |
| H5: Género diferente entre grupos | Chi-cuadrado | ✅ Se rechaza H0 |

### 4. Evaluación del Experimento
- **Design Effectiveness**: grupos demográficamente comparables ✅
- **Duration**: 97 días (~14 semanas) — suficiente ✅
- **Additional Data Needs**: tipo de dispositivo, canal de entrada, errores reales

---

## Principales hallazgos
| KPI | Control | Test | Conclusión |
|---|---|---|---|
| Completion Rate | 62.11% | 61.95% | Mejora significativa (H1 ✅) pero mínima |
| Umbral rentabilidad (+5%) | — | — | No alcanzado ❌ |
| Backtracking | ~38% | ~43% | Test tiene más errores ⚠️ |

- El nuevo diseño **mejora significativamente** la tasa de finalización (H1 ✅)
- Sin embargo, **no supera el umbral del 5%** necesario para ser rentable (H2 ❌)
- El grupo Test presenta **mayor tasa de backtracking** → hay puntos de fricción en la nueva UI
- Se detectaron **diferencias demográficas** entre grupos (edad y género) que podrían introducir sesgo

---

## Dashboard Tableau
El archivo `Proyecto_Control_Test.twbx` contiene el dashboard interactivo con las siguientes visualizaciones:
- Embudo de conversión Control vs Test
- Completion Rate por grupo y por género
- Drop-off por paso
- Distribución de edad (Control vs Test)
- Backtracking por grupo
- Años con Vanguard
- Distribución de género

---

## Recomendaciones para Vanguard
- ✅ Mantener el nuevo diseño dado que mejora la conversión
- 🔧 Optimizar los pasos con más retrocesos (especialmente `step_1` y `step_2`)
- 📊 Recopilar datos adicionales: tipo de dispositivo, canal de entrada, errores reales
- 🔁 Implementar futuras pruebas A/B con grupos más homogéneos (50/50)
- 💰 Realizar un análisis de ROI completo antes de escalar el rediseño

---

## Tecnologías utilizadas
- **Python 3.10** — análisis de datos
- **Pandas / NumPy** — manipulación de datos
- **Matplotlib / Seaborn** — visualización
- **SciPy / Statsmodels** — pruebas estadísticas
- **Tableau Desktop** — dashboard interactivo

---

## Instalación y uso
```bash
# Clonar el repositorio
git clone https://github.com/demonvaa/vanguard-ab-test.git
cd vanguard-ab-test

# Instalar dependencias
pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter

# Ejecutar el notebook
jupyter notebook Proyecto_2.ipynb
```

---

## Equipo
| Nombre | GitHub |
|---|---|
| Ernesto Vaamonde | [@demonvaa](https://github.com/demonvaa) |
| Salvador Ciaurriz | [@salvadorciaurriz-lang](https://github.com/salvadorciaurriz-lang) |

---

## Fuentes de datos
- Datos proporcionados por [Ironhack Data Analytics Bootcamp](https://www.ironhack.com)
