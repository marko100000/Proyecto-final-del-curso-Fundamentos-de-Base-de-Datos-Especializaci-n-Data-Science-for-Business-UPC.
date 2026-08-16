# Segmentación de Clientes de Seguros con K-Means

Proyecto de análisis y segmentación de clientes desarrollado utilizando el dataset **IBM Watson Marketing Customer Value Data**.

El objetivo principal del proyecto es identificar grupos homogéneos de clientes de una compañía de seguros mediante técnicas de **Machine Learning no supervisado**, específicamente el algoritmo **K-Means**, con la finalidad de generar información útil para estrategias comerciales, fidelización, retención y gestión de riesgo.

---

## 📌 Descripción del proyecto

La base de datos contiene información de **9,134 clientes** de una compañía de seguros, incluyendo variables financieras, de comportamiento y características demográficas.

El problema planteado consiste en que la empresa no cuenta con una segmentación adecuada de sus clientes que permita diferenciar sus características y diseñar estrategias específicas para cada grupo.

Para abordar este problema se desarrolló un proceso de segmentación utilizando **K-Means**, evaluando distintas configuraciones del modelo y seleccionando aquella que presentó una mejor separación entre los grupos.

---

## 🎯 Objetivo general

Aplicar el algoritmo **K-Means** para segmentar a los clientes en grupos homogéneos según su comportamiento financiero y de consumo del seguro, permitiendo diseñar estrategias comerciales, de retención y de gestión de riesgo diferenciadas por segmento.

### Objetivos específicos

* Determinar el número óptimo de clústeres mediante el **coeficiente de Silhouette**.
* Caracterizar cada segmento según variables financieras y de comportamiento.
* Analizar diferentes tratamientos de las variables numéricas.
* Comparar distintas configuraciones del modelo K-Means.
* Utilizar variables categóricas para interpretar y perfilar los segmentos obtenidos.
* Traducir los resultados del modelo en recomendaciones de negocio.

---

## 📂 Estructura del repositorio

```text
segmentacion-clientes-seguros-kmeans/
│
├── README.md
│
├── data/
│   └── customer.csv
│
├── notebooks/
│   └── EF_MARKO_NAVEDA.ipynb
│
└── presentation/
    └── EF_MARKO_NAVEDA.pptx
```

### Archivos principales

* `data/customer.csv`
  Dataset utilizado para realizar el análisis y la segmentación.

* `notebooks/EF_MARKO_NAVEDA.ipynb`
  Notebook que contiene el análisis exploratorio, preparación de datos, construcción de modelos, evaluación y segmentación de clientes.

* `presentation/EF_MARKO_NAVEDA.pptx`
  Presentación final del proyecto con los principales resultados, conclusiones y recomendaciones estratégicas.

---

## 📊 Dataset

El dataset utilizado corresponde a **IBM Watson Marketing Customer Value Data** y contiene información de **9,134 clientes**.

Para el modelo principal se utilizaron cuatro variables numéricas.

| Variable                | Descripción                          | Promedio | Rango aproximado |
| ----------------------- | ------------------------------------ | -------: | ---------------: |
| `CustomerLifetimeValue` | Valor económico estimado del cliente |    8,005 |   1,898 – 83,325 |
| `Income`                | Ingreso del cliente                  |   37,657 |       0 – 99,981 |
| `MonthlyPremiumAuto`    | Prima mensual del seguro             |       93 |         61 – 298 |
| `ClaimAmount`           | Monto de reclamaciones               |      434 |        0 – 2,893 |

Las variables presentaban escalas diferentes y presencia de valores atípicos, por lo que fue necesario aplicar procesos de transformación y estandarización antes del entrenamiento de los modelos.

---

## 🧩 Variables categóricas

Las variables categóricas no participaron directamente en el cálculo de K-Means, pero fueron utilizadas posteriormente para interpretar los segmentos obtenidos.

Entre ellas se encuentran:

* `Coverage`
* `EmploymentStatus`
* `Gender`
* `MaritalStatus`
* `SalesChannel`
* `VehicleClass`

Estas variables permitieron construir un perfil más completo de cada grupo y transformar los resultados técnicos del modelo en información útil para la toma de decisiones.

---

## ⚙️ Metodología

El proyecto siguió de manera general las siguientes etapas:

### 1. Exploración de los datos

Se realizó una revisión de las variables del dataset, sus distribuciones, escalas y presencia de valores atípicos.

Las cuatro variables principales utilizadas en el modelo no presentaban valores nulos.

### 2. Preparación de los datos

Debido a que K-Means utiliza distancias para asignar observaciones a los clústeres, fue necesario estandarizar las variables numéricas.

También se analizaron alternativas para tratar la asimetría y los valores extremos presentes en los datos.

### 3. Construcción de modelos

Se evaluaron cuatro configuraciones diferentes:

1. Modelo con 8 variables.
2. Modelo con 4 variables principales.
3. Modelo de 4 variables aplicando **winsorización**.
4. Modelo de 4 variables aplicando **transformación logarítmica**.

### 4. Selección del número de clústeres

Para cada modelo se evaluaron distintos valores de `k`.

La selección se realizó utilizando el **coeficiente de Silhouette**, que permite evaluar qué tan similares son las observaciones dentro de un mismo clúster y qué tan diferentes son respecto a otros grupos.

### 5. Visualización mediante PCA

Se utilizó **Análisis de Componentes Principales (PCA)** para reducir la dimensionalidad de los datos y visualizar gráficamente la separación entre los clústeres.

### 6. Comparación de modelos

Los modelos fueron comparados de acuerdo con su índice de Silhouette y la proporción de observaciones con valores de silueta negativos.

---

## 📈 Comparación de modelos

| Modelo                                   | Mejor índice de Silhouette | Siluetas negativas |
| ---------------------------------------- | -------------------------: | -----------------: |
| 8 variables                              |                      0.216 |              8.13% |
| **4 variables**                          |                  **0.380** |              7.13% |
| 4 variables + Winsorización              |                      0.320 |          **3.55%** |
| 4 variables + Transformación logarítmica |                      0.267 |              6.07% |

El modelo seleccionado fue el modelo de **4 variables**, al presentar el mayor índice de Silhouette entre las alternativas evaluadas.

El valor óptimo obtenido fue:

```text
k = 2
```

Por lo tanto, los clientes fueron agrupados en **dos segmentos principales**.

---

# 👥 Segmentación obtenida

El modelo permitió identificar dos grupos claramente diferenciados:

1. **Clientes conservadores**
2. **Clientes de alto valor**

---

## 🔵 Segmento 1 — Clientes conservadores

Representan aproximadamente:

```text
7,149 clientes
78.3% de la cartera
```

### Características promedio

| Indicador               |     Valor |
| ----------------------- | --------: |
| Customer Lifetime Value |  6,323.30 |
| Income                  | 41,573.48 |
| Monthly Premium Auto    |     81.26 |
| Claim Amount            |    334.79 |

### Perfil predominante

* Cobertura: **Basic**
* Situación laboral: **Employed**
* Género: **F**
* Estado civil: **Married**
* Canal de venta: **Agent**
* Vehículo: **Four-Door Car**

Este grupo representa la mayor parte de la cartera, pero presenta un **Customer Lifetime Value promedio menor**.

---

## 🟢 Segmento 2 — Clientes de alto valor

Representan aproximadamente:

```text
1,985 clientes
21.7% de la cartera
```

### Características promedio

| Indicador               |     Valor |
| ----------------------- | --------: |
| Customer Lifetime Value | 14,061.38 |
| Income                  | 23,553.49 |
| Monthly Premium Auto    |    136.28 |
| Claim Amount            |    791.72 |

### Perfil predominante

* Cobertura: **Extended**
* Situación laboral: **Unemployed**
* Género: **F**
* Estado civil: **Married**
* Canal de venta: **Agent**
* Vehículo: **SUV**

A pesar de representar solamente el **21.7% de los clientes**, este grupo presenta un Customer Lifetime Value promedio superior al doble del observado en el segmento conservador.

---

# 💡 Principal hallazgo

Uno de los principales resultados del análisis es que:

> **El segmento de clientes de alto valor es considerablemente más pequeño, pero genera un valor económico mucho mayor para la empresa.**

El grupo representa aproximadamente **21.7% de la cartera**, pero presenta un **Customer Lifetime Value promedio de 14,061.38**, frente a aproximadamente **6,323.30** en los clientes conservadores.

Además, su prima mensual promedio asciende a **136.28**, frente a **81.26** en el segmento conservador.

Estos resultados muestran que tratar a todos los clientes bajo una misma estrategia comercial podría generar una asignación poco eficiente de los recursos.

---

# 💼 Recomendaciones estratégicas

A partir de la segmentación obtenida se proponen distintas acciones de negocio.

## 1. Priorizar clientes de alto valor

Asignar mayor atención comercial a los clientes que generan mayor valor y presentan mayor potencial económico.

Acciones sugeridas:

* Crear una lista priorizada de clientes de alto valor.
* Asignar seguimiento comercial personalizado.
* Analizar rentabilidad y permanencia de estos clientes.
* Priorizar oportunidades de renovación y ampliación de productos.

**Indicador sugerido:**
Customer Lifetime Value por cliente y participación en ventas.

---

## 2. Fortalecer la fidelización

Desarrollar estrategias específicas para retener a los clientes de mayor valor.

Acciones sugeridas:

* Implementar atención preferencial.
* Desarrollar estrategias de postventa.
* Ofrecer beneficios por permanencia o renovación.
* Anticipar reclamos y necesidades.
* Crear alertas para clientes con riesgo de abandono.

**Indicador sugerido:**
Tasa de renovación y retención.

---

## 3. Captar clientes similares

Utilizar las características del segmento de alto valor para identificar nuevos clientes potenciales.

Acciones sugeridas:

* Utilizar el perfil del cliente de alto valor como mercado objetivo.
* Orientar campañas hacia clientes con cobertura Extended.
* Potenciar el canal de agentes.
* Construir bases de prospectos con características similares.

**Indicador sugerido:**
Cantidad de nuevos clientes similares al segmento de alto valor.

---

## 4. Gestionar eficientemente el segmento conservador

El segmento conservador representa aproximadamente el **78.3% de la cartera**, por lo que requiere estrategias escalables y eficientes.

Acciones sugeridas:

* Automatizar campañas de comunicación y renovación.
* Ofrecer productos básicos y upgrades progresivos.
* Detectar clientes con potencial para migrar hacia el segmento de alto valor.
* Controlar el costo de atención por cliente.

**Indicador sugerido:**
Costo de atención por cliente conservador.

---

## 5. Aplicar campañas diferenciadas

La segmentación evidencia que una única estrategia comercial para todos los clientes no sería la opción más eficiente.

Se recomienda desarrollar propuestas específicas para cada segmento:

### Clientes de alto valor

* Atención personalizada.
* Productos premium.
* Estrategias de fidelización.
* Beneficios exclusivos.
* Seguimiento comercial directo.

### Clientes conservadores

* Comunicación automatizada.
* Productos simples y económicos.
* Campañas masivas.
* Estrategias de cross-selling y upgrade.

**Indicador sugerido:**
Conversión por campaña y segmento.

---

# 🧠 Técnicas utilizadas

Durante el desarrollo del proyecto se aplicaron conceptos y técnicas relacionadas con:

* Análisis exploratorio de datos.
* Preparación y limpieza de datos.
* Estandarización de variables.
* Tratamiento de valores atípicos.
* Winsorización.
* Transformaciones logarítmicas.
* Machine Learning no supervisado.
* K-Means Clustering.
* Coeficiente de Silhouette.
* Principal Component Analysis (PCA).
* Segmentación de clientes.
* Perfilamiento de clústeres.
* Interpretación de resultados desde una perspectiva de negocio.

---

# 🛠️ Tecnologías

* Python
* Jupyter Notebook
* Análisis de datos
* Machine Learning
* Clustering
* K-Means
* PCA

---

# 📌 Conclusiones

La aplicación del algoritmo **K-Means** permitió identificar grupos diferenciados dentro de los 9,134 clientes analizados.

La comparación entre distintas configuraciones permitió seleccionar un modelo de cuatro variables con dos clústeres como alternativa principal para la segmentación.

Los resultados permitieron identificar dos perfiles relevantes:

* **Clientes conservadores:** representan la mayor parte de la cartera y presentan un menor valor promedio por cliente.
* **Clientes de alto valor:** representan una proporción menor, pero poseen un Customer Lifetime Value y una prima mensual considerablemente superiores.

La incorporación de variables categóricas permitió complementar la segmentación y construir perfiles comerciales más interpretables.

Finalmente, el análisis demuestra cómo una técnica de Machine Learning no supervisado puede convertirse en una herramienta útil para apoyar decisiones relacionadas con:

* Captación de clientes.
* Fidelización.
* Retención.
* Segmentación de campañas.
* Priorización comercial.
* Gestión del riesgo.
* Asignación eficiente de recursos.

---

# 👨‍💻 Integrantes

Proyecto desarrollado por:

* **Julio López Talavera**
* **Marko Naveda Samamé**
* **Victor Pineda Alvarado**
* **Rodrigo Arestegui Condor**

---

# 🎓 Contexto académico

Proyecto desarrollado como parte de la formación académica en **Data Science for Business**.

El proyecto busca integrar conceptos de análisis de datos, Machine Learning y estrategia empresarial para transformar información en recomendaciones orientadas a la toma de decisiones.

---

# 📁 Recursos del proyecto

📊 **Dataset:**
[`customer.csv`](data/customer.csv)

📓 **Notebook:**
[`EF_MARKO_NAVEDA.ipynb`](notebooks/EF_MARKO_NAVEDA.ipynb)

📑 **Presentación:**
[`EF_MARKO_NAVEDA.pptx`](presentation/EF_MARKO_NAVEDA.pptx)

---

## Autor

**Marko Naveda Samamé**

Data Science for Business
Universidad Peruana de Ciencias Aplicadas — UPC

---

⭐ Si este proyecto te resulta interesante, puedes explorar el notebook para revisar en detalle el proceso de preparación de datos, construcción de modelos y segmentación de clientes.
