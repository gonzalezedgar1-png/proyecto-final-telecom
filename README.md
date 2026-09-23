# 📞 Proyecto Final — Telecomunicaciones: Identificación de operadores ineficaces

## 📌 Descripción del proyecto

CallMeMaybe es un servicio de telefonía virtual utilizado por organizaciones para gestionar llamadas entrantes, salientes e internas entre operadores.

El objetivo de este proyecto es analizar los datos de llamadas y **identificar operadores que presentan señales de ineficiencia**, considerando principalmente:

- Una elevada cantidad o proporción de llamadas entrantes perdidas.
- Un tiempo de espera elevado para llamadas entrantes.
- Un bajo volumen de llamadas salientes cuando el puesto del operador requiere realizar llamadas outbound.

Además, se realiza un análisis exploratorio de los datos, pruebas de hipótesis estadísticas y la preparación de dashboards para facilitar el análisis del desempeño de los operadores.

---

## 🎯 Objetivos

1. Realizar un análisis exploratorio de los datos.
2. Limpiar y preparar los datasets.
3. Analizar el comportamiento de las llamadas entrantes, salientes, internas y externas.
4. Crear métricas de desempeño por operador.
5. Identificar operadores que presentan señales de ineficiencia.
6. Evaluar hipótesis estadísticas relacionadas con los planes tarifarios.
7. Crear dashboards interactivos para visualizar los resultados.
8. Presentar conclusiones y recomendaciones basadas en los datos.

---

## 📂 Datasets

El proyecto utiliza dos datasets proporcionados para el proyecto:

### `telecom_dataset_new.csv`

Contiene información sobre las llamadas realizadas mediante el servicio CallMeMaybe.

Principales variables:

| Variable | Descripción |
|---|---|
| `user_id` | Identificador del cliente |
| `date` | Fecha de registro de las estadísticas |
| `direction` | Dirección de la llamada: entrante o saliente |
| `internal` | Indica si la llamada es interna |
| `operator_id` | Identificador del operador |
| `is_missed_call` | Indica si la llamada fue perdida |
| `calls_count` | Número de llamadas |
| `call_duration` | Duración de la conversación |
| `total_call_duration` | Duración total incluyendo espera |

### `telecom_clients.csv`

Contiene información sobre los clientes:

| Variable | Descripción |
|---|---|
| `user_id` | Identificador del cliente |
| `tariff_plan` | Plan tarifario |
| `date_start` | Fecha de inicio del servicio |

---

## 🧹 Limpieza y preparación de datos

Durante el análisis se realizaron diferentes controles de calidad:

- Eliminación de registros duplicados.
- Conversión de la columna `date` al formato datetime.
- Exclusión de registros sin `operator_id` para el análisis individual de operadores.
- Revisión de valores ausentes.
- Identificación de inconsistencias en `is_missed_call`.
- Creación de la variable `wait_duration`.
- Identificación de registros anómalos relacionados con una cantidad excesiva de tiempo registrado por operador y día.

Se encontraron **296 registros donde una llamada estaba marcada como perdida pero presentaba duración de conversación positiva**. Estos registros fueron revisados y recodificados como llamadas atendidas.

También se identificaron operadores con registros diarios anómalos, los cuales fueron excluidos del análisis de desempeño para evitar que distorsionaran los resultados.

---

## 🔎 Análisis exploratorio

El análisis exploratorio incluye:

### Distribución de duración de llamadas

Se analizó la distribución de `call_duration` mediante un histograma para identificar patrones, concentración de valores y posibles valores extremos.

### Llamadas internas y externas

Se analizó la proporción de llamadas internas frente a externas.

### Llamadas entrantes y salientes

Se comparó el volumen de actividad según la dirección de las llamadas.

### Volumen diario

Se calculó el número total de llamadas por día para analizar la variación del volumen de trabajo.

---

## 📊 Métricas por operador

Para identificar posibles problemas de desempeño se calcularon las siguientes métricas:

### Llamadas entrantes

Número total de llamadas recibidas por cada operador.

### Llamadas entrantes perdidas

Número de llamadas entrantes que no fueron atendidas.

### Tasa de llamadas perdidas

```text
Tasa de llamadas perdidas =
llamadas perdidas / llamadas entrantes
