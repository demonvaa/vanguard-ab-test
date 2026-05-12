🟩 1. Cargar y preparar los datasets
Objetivo: tener un dataset limpio, unido y listo para análisis.

Datasets:

df_final_demo → datos demográficos

df_final_web_data_pt1 + pt2 → comportamiento digital

df_final_experiment_clients → asignación a control/test

Tareas:

Cargar los 3 datasets

Unir pt1 + pt2

Revisar duplicados

Revisar tipos de datos

Convertir date_time a datetime

Unir datasets por client_id y/o visitor_id

Crear columna completion_flag (si llega al paso final)

🟩 2. EDA & Data Cleaning (Día 1–2)
Demografía
Distribución de edad

Distribución de género

Tenure (años/meses)

Número de cuentas

Balance

Comportamiento digital
Número de pasos completados

Tiempos entre pasos

Abandonos por paso

Diferencias entre control vs test (sin hipótesis aún)

Limpieza
Valores nulos

Outliers (balance, edad, logins, llamadas)

Consistencia de pasos (1→2→3→confirm)

🟩 3. Performance Metrics (Día 3)
KPIs recomendados:

1. Completion Rate
𝐶
𝑅
=
clientes que llegan a confirmaci
o
ˊ
n
clientes que inician
2. Drop-off por paso
𝐷
𝑟
𝑜
𝑝
_
𝑠
𝑡
𝑒
𝑝
_
𝑖
=
1
−
𝑁
𝑖
+
1
𝑁
𝑖
3. Tiempo medio por paso
4. Engagement
logons_6_mnth

calls_6_mnth

Comparación Control vs Test
CR

Drop-off

Tiempo total

Tiempo por paso

🟩 4. Hypothesis Testing (Día 4–5)
H1: El nuevo diseño aumenta la tasa de finalización
Test: proporciones (z-test)

𝐻
0
:
𝑝
𝑡
𝑒
𝑠
𝑡
=
𝑝
𝑐
𝑜
𝑛
𝑡
𝑟
𝑜
𝑙
𝐻
1
:
𝑝
𝑡
𝑒
𝑠
𝑡
>
𝑝
𝑐
𝑜
𝑛
𝑡
𝑟
𝑜
𝑙
H2: Cost-effectiveness threshold
Si el rediseño cuesta X, ¿compensa el aumento de conversiones?

H3: Otros tests opcionales
Diferencias en tiempo por paso

Diferencias por edad

Diferencias por tenure

Diferencias por balance

🟩 5. Experiment Evaluation
1. Diseño
¿Hubo randomización real?

¿Hay diferencias demográficas entre grupos?

¿Hay sesgos por dispositivo/visit_id?

2. Duración
¿3 meses es suficiente?

¿Hay estacionalidad?

3. Datos adicionales necesarios
Tipo de dispositivo

Canal de entrada

Información de errores

Tiempo real por paso

🟩 6. Tableau (Día 1–2 Semana 6)
Dashboards recomendados:

Funnel Control vs Test

Completion Rate por demografía

Drop-off por paso

Heatmap de tiempos

Segmentación por edad / balance / tenure

🟩 7. Presentación (Día 3–4 Semana 6)
Estructura recomendada:

Título

Contexto del experimento

Datasets

EDA

KPIs

Hypothesis Testing

Evaluación del experimento

Tableau

Conclusiones

Recomendaciones

Trabajo en equipo

