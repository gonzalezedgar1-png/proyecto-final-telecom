# 📞 Proyecto Final — Telecomunicaciones: Identificación de operadores ineficaces

## CallMeMaybe

Análisis de datos de una empresa de telecomunicaciones para identificar operadores con posibles señales de ineficiencia en la atención de llamadas, utilizando análisis exploratorio, métricas de desempeño, pruebas estadísticas y dashboards interactivos.

---

## 📌 Descripción del proyecto

Este proyecto analiza los datos de llamadas de **CallMeMaybe**, una empresa de telecomunicaciones.

El objetivo principal es identificar operadores que presentan señales consistentes de desempeño problemático, especialmente en llamadas entrantes, considerando indicadores como:

- Tasa de llamadas perdidas.
- Tiempo promedio de espera.
- Volumen de llamadas entrantes.
- Volumen de llamadas salientes.
- Plan tarifario.
- Comportamiento diario de las llamadas.

El análisis combina técnicas de **Python, Pandas, SciPy y Tableau Public** para transformar los datos originales en información útil para la toma de decisiones operativas.

> **Nota:** los operadores identificados se consideran casos prioritarios para revisión y no necesariamente como evidencia de bajo desempeño individual. Las métricas deben interpretarse considerando carga de trabajo, turnos, distribución de llamadas y funciones específicas de cada operador.
>
> # 🎯 Objetivos

## Objetivo general

Identificar operadores que presentan señales de ineficiencia en la gestión de llamadas y proporcionar información que permita investigar posibles problemas operativos.

## Objetivos específicos

1. Limpiar y preparar los datos de llamadas.
2. Analizar el volumen y comportamiento de las llamadas.
3. Comparar llamadas entrantes y salientes.
4. Calcular métricas de desempeño por operador.
5. Identificar operadores con alta tasa de llamadas perdidas y alta espera.
6. Utilizar el volumen outbound como señal complementaria.
7. Realizar pruebas estadísticas sobre las diferencias entre planes tarifarios.
8. Crear dashboards interactivos en Tableau Public.
9. Presentar conclusiones y recomendaciones basadas en los datos.

10. # 📊 Datos utilizados

## Dataset de llamadas

El dataset contiene información relacionada con las llamadas realizadas y recibidas por los operadores.

| Variable | Descripción |
|---|---|
| `user_id` | Identificador del cliente |
| `date` | Fecha y hora de la llamada |
| `direction` | Dirección de la llamada: entrante o saliente |
| `internal` | Indicador de llamada interna |
| `operator_id` | Identificador del operador |
| `is_missed_call` | Indica si la llamada fue perdida |
| `calls_count` | Número de llamadas representadas por el registro |
| `call_duration` | Duración de la llamada |
| `total_call_duration` | Duración total incluyendo espera |

## Dataset de clientes

Contiene información relacionada con los clientes.

| Variable | Descripción |
|---|---|
| `user_id` | Identificador del cliente |
| `tariff_plan` | Plan tarifario |
| `date_start` | Fecha de inicio del servicio |

# 🗂️ Archivos del proyecto

El repositorio contiene los siguientes archivos principales:

| Archivo | Descripción |
|---|---|
| `telecom_final_analysis.ipynb` | Notebook principal del análisis |
| `telecom_dashboard_data.csv` | Dataset preparado para Tableau |
| `telecom_operator_metrics.csv` | Métricas calculadas por operador |
| `telecom_ineffective_operators.csv` | Operadores prioritarios identificados |
| `Proyecto_Final_Telecom_CallMeMaybe.pdf` | Presentación final del proyecto |
| `README.md` | Documentación del proyecto |

### `telecom_final_analysis.ipynb`

Incluye:

- Importación de datos.
- Limpieza.
- Preparación.
- Análisis exploratorio.
- Métricas por operador.
- Identificación de operadores prioritarios.
- Pruebas estadísticas.

### `telecom_operator_metrics.csv`

Contiene las métricas calculadas por operador:

- Llamadas entrantes.
- Llamadas perdidas.
- Tiempo de espera.
- Tasa de llamadas perdidas.
- Espera promedio.
- Llamadas salientes.
- Plan tarifario.
- Indicadores de riesgo.

### `telecom_ineffective_operators.csv`

Contiene los operadores identificados como casos prioritarios de acuerdo con los criterios establecidos en el análisis.

### `telecom_dashboard_data.csv`

Dataset preparado específicamente para Tableau Public.

Incluye campos adicionales como:

- `Call Type`
- `Direction Label`
- `Date Day`
- `Duration Minutes`
- `Wait Seconds`
- `Call Duration (bin)`

### `Proyecto_Final_Telecom_CallMeMaybe.pdf`

Presentación final con metodología, resultados, operadores prioritarios, pruebas estadísticas, dashboards y conclusiones.


# 🧹 Limpieza y preparación de datos

El dataset original contenía **53,902 registros de llamadas** y **732 clientes**.

| Control | Resultado |
|---|---:|
| Registros iniciales | 53,902 |
| Duplicados eliminados | 4,900 |
| Operador faltante | 7,456 (13.8%) |
| Inconsistencias `is_missed_call` corregidas | 296 |
| Operadores con días >12 h eliminados | 7 |
| Filas finales para análisis | 40,658 |

### Procesos realizados

**1. Eliminación de duplicados**

Se identificaron y eliminaron 4,900 registros duplicados.

**2. Operadores faltantes**

Se encontraron 7,456 registros sin `operator_id`, equivalentes aproximadamente al 13.8% del dataset original.

Estos registros fueron excluidos del análisis individual de operadores porque no era posible atribuirlos a un operador específico.

**3. Corrección de inconsistencias**

Se encontraron 296 registros donde `is_missed_call = True`, pero la duración de la llamada era positiva.

Estos registros fueron recodificados como llamadas atendidas.

**4. Cálculo del tiempo de espera**

Se creó la variable:

```text
wait_duration = total_call_duration - call_duration


---

## 6. EDA

```markdown
# 🔎 Análisis exploratorio de datos (EDA)

El periodo analizado comprende:

**2 de agosto de 2019 — 28 de noviembre de 2019**

equivalente a **118 días**.

## Principales indicadores

| Indicador | Resultado |
|---|---:|
| Registros finales | 40,658 |
| Operadores analizados | 1,085 |
| Clientes | 732 |
| Llamadas totales | 515,251 |
| Llamadas entrantes | 89,882 |
| Llamadas salientes | 425,369 |
| Porcentaje entrantes | 17.4% |
| Porcentaje salientes | 82.6% |
| Tasa global de llamadas entrantes perdidas | 0.54% |
| Espera media entrante | 13.45 s |
| Mediana de duración | 105 s |

El volumen de llamadas está claramente dominado por las llamadas salientes.

Sin embargo, la tasa global de llamadas entrantes perdidas es relativamente baja, por lo que el análisis de operadores se enfocó en detectar aquellos casos que se alejan considerablemente del comportamiento general.

## Distribución de duración

La distribución de la duración de las llamadas presenta una **cola derecha marcada**, indicando que existen algunas llamadas considerablemente más largas que la mayoría.

Para facilitar la interpretación visual de los gráficos, algunas visualizaciones utilizan el percentil 99 como límite visual.

Esto permite observar mejor la concentración principal de los datos sin eliminar las observaciones originales del análisis.


# 👥 Métricas por operador

Para evaluar el desempeño individual se calcularon las siguientes métricas.

| Métrica | Descripción |
|---|---|
| `incoming_calls` | Número total de llamadas entrantes |
| `missed_calls` | Número de llamadas entrantes perdidas |
| `missed_rate` | Tasa de llamadas perdidas |
| `avg_wait_sec` | Tiempo promedio de espera en segundos |
| `outgoing_calls` | Número total de llamadas salientes |

### Tasa de llamadas perdidas

```text
missed_rate = missed_calls / incoming_calls

avg_wait_sec = wait_seconds / incoming_calls


---

## 8. Identificación de operadores prioritarios

```markdown
# ⚠️ Identificación de operadores prioritarios

Para evitar conclusiones inestables basadas en operadores con muy pocas llamadas, se estableció un mínimo de:

**20 llamadas entrantes.**

Los umbrales utilizados fueron:

```text
incoming_calls >= 20

missed_rate >= 0.66%

avg_wait_sec >= 20.80 segundos


---

## 9. Señal outbound

```markdown
# 📤 Señal complementaria: llamadas salientes

Además de las métricas entrantes, se utilizó el volumen outbound como una señal secundaria.

El umbral utilizado fue:

```text
outgoing_calls <= 58


---

## 10. Pruebas estadísticas

```markdown
# 🧪 Pruebas estadísticas

Se realizaron pruebas estadísticas para evaluar si existían diferencias entre los planes tarifarios **A, B y C**.

Para evitar que operadores con muy pocas llamadas distorsionaran los resultados, se utilizaron operadores con:

```text
incoming_calls >= 20
H = 8.21
p = 0.0165
α = 0.05

H = 0.31
p = 0.8561
α = 0.05


---

## 11. Dashboards Tableau

```markdown
# 📊 Dashboards interactivos

Los dashboards fueron desarrollados utilizando **Tableau Public**.

## Dashboard 1 — Análisis de llamadas

Incluye:

- Histograma de duración de llamadas.
- Distribución de llamadas internas y externas.
- Filtro por dirección de llamada.
- Comparación entre llamadas entrantes y salientes.

## Dashboard 2 — Volumen de llamadas

Incluye:

- Volumen de llamadas por día.
- Distribución de llamadas internas y externas.
- Filtro por tipo de llamada.
- Evolución diaria del volumen de llamadas.

### 🔗 Tableau Public

[Ver proyecto interactivo en Tableau Public](https://public.tableau.com/app/profile/edgar.adrian.gonzalez8050/viz/ProyectoFinalTelecom-CallMeMaybe/Dashboard1Anlisisdellamadas)

# 🛠️ Tecnologías utilizadas

### Python

- Python
- Pandas
- NumPy
- SciPy
- Jupyter Notebook
- Matplotlib

### Visualización

- Tableau Public

### Control de versiones

- Git
- GitHub

# 📐 Metodología

El flujo de trabajo utilizado fue:

```text
Datos originales
       ↓
Limpieza
       ↓
Corrección de inconsistencias
       ↓
Integración de datasets
       ↓
Análisis exploratorio
       ↓
Métricas por operador
       ↓
Identificación de operadores prioritarios
       ↓
Pruebas estadísticas
       ↓
Visualización en Tableau
       ↓
Conclusiones


---

## 14. Conclusiones

```markdown
# 💡 Conclusiones

1. Después de la limpieza se obtuvieron **40,658 registros** para el análisis y **1,085 operadores**.

2. El volumen de llamadas está dominado por las llamadas salientes, que representan aproximadamente el **82.6%** del total.

3. La tasa global de llamadas entrantes perdidas es de **0.54%**, aunque este promedio oculta diferencias importantes entre operadores.

4. Se identificaron **29 operadores** que presentan simultáneamente una tasa elevada de llamadas perdidas y una espera promedio elevada.

5. **14 de estos operadores** también presentan un volumen outbound igual o inferior a 58 llamadas. Este indicador debe interpretarse considerando las responsabilidades del puesto.

6. Las pruebas estadísticas muestran evidencia de diferencias en la espera media entre los planes tarifarios.

7. La comparación post hoc encontró evidencia estadística de diferencia entre los planes A y B bajo la metodología utilizada.

8. No se encontró evidencia estadística suficiente para afirmar que la tasa de llamadas perdidas difiera entre los planes A, B y C.

9. Los operadores identificados deben considerarse **casos prioritarios para investigación**, no como evaluaciones definitivas de desempeño individual.

10. Los resultados pueden utilizarse para orientar una revisión operativa más detallada, considerando factores como turnos, carga de trabajo, distribución de llamadas y responsabilidades específicas.

# 📎 Entregables

| Archivo | Descripción |
|---|---|
| `telecom_final_analysis.ipynb` | Notebook completo del análisis |
| `telecom_dashboard_data.csv` | Dataset preparado para Tableau |
| `telecom_operator_metrics.csv` | Métricas calculadas por operador |
| `telecom_ineffective_operators.csv` | Operadores prioritarios identificados |
| `Proyecto_Final_Telecom_CallMeMaybe.pdf` | Presentación final |
| `README.md` | Documentación del proyecto |

# 📚 Fuentes consultadas

### NIST/SEMATECH — Exploratory Data Analysis

Referencia utilizada para metodología de análisis exploratorio, detección de anomalías y revisión de distribuciones.

https://www.nist.gov/publications/nistsematech-e-handbook-statistical-methods-chapter-1-exploratory-data-analysis

### NIST — Histogram Interpretation

Referencia para interpretar histogramas, asimetrías, colas y valores extremos.

https://www.itl.nist.gov/div898/handbook/eda/section3/eda33d.htm

### SciPy — Kruskal-Wallis

Documentación utilizada para la aplicación de la prueba no paramétrica de Kruskal-Wallis.

https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.kruskal.html

### SciPy — Mann-Whitney U

Documentación utilizada para las comparaciones estadísticas por pares.

https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.mannwhitneyu.html

### Pandas — groupby

Referencia utilizada para la agregación de métricas por operador.

https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html

### Pandas — to_datetime

Referencia utilizada para la transformación y manejo de variables de fecha.

https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html

### Tableau — Build a Histogram

Referencia para la creación de histogramas y bins en Tableau.

https://help.tableau.com/current/pro/desktop/en-us/buildexamples_histogram.htm

### Tableau — Filtering

Referencia para la creación y aplicación de filtros interactivos.

https://help.tableau.com/current/pro/desktop/en-gb/filtering.htm

# 👤 Autor

**Edgar Adrian Gonzalez Perez**

Data Analyst

Proyecto realizado como parte del programa de formación en análisis de datos.
