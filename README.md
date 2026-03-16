
# 🛒 Análisis de Ventas E-commerce y Data Warehouse (BigQuery)

## 📌 Descripción del Proyecto

Este proyecto implementa un flujo de análisis de datos para estudiar el comportamiento de ventas en un marketplace de comercio electrónico.

El objetivo es transformar datos transaccionales en **información útil para la toma de decisiones**, utilizando un enfoque básico de **Data Warehouse con BigQuery** y análisis exploratorio en **Python**.

El análisis permite identificar:

* 🏆 Productos más vendidos
* 💰 Tendencias de ingresos
* 📦 Rendimiento por categoría
* 👥 Patrones de compra de los clientes

Este proyecto simula cómo un **analista de datos trabaja con información almacenada en la nube y la analiza posteriormente con herramientas de ciencia de datos**.

---

# ☁️ Tecnologías Utilizadas

## Infraestructura Cloud

* ☁️ Google Cloud Platform
* 🗄️ Google Cloud Storage
* 📊 BigQuery

## Análisis de Datos

* 🐍 Python
* 🐼 Pandas
* 📈 Matplotlib
* 🎨 Seaborn

## Lenguaje de Consulta

* 🧠 SQL

---

# 📊 Dataset

El proyecto utiliza el dataset público:

**Brazilian E-Commerce Public Dataset by Olist**

Este conjunto de datos contiene transacciones reales de un marketplace brasileño.

### Tablas principales utilizadas

| Tabla       | Descripción                       |
| ----------- | --------------------------------- |
| orders      | Información de las órdenes        |
| order_items | Productos incluidos en cada orden |
| customers   | Información de clientes           |
| products    | Catálogo de productos             |

### Características del dataset

* 📦 Más de **100,000 órdenes**
* 🛍️ Múltiples categorías de productos
* 🚚 Información de costos de envío
* 👤 Datos de clientes

---

# 🏗️ Arquitectura del Proyecto

El proyecto sigue un flujo simple de análisis de datos:

```
Archivos CSV
     ↓
☁️ Google Cloud Storage
     ↓
📊 BigQuery (Dataset)
     ↓
🧠 Consultas SQL
     ↓
🐍 Análisis en Python
     ↓
📈 Visualizaciones e Insights
```

En este proyecto, **Google Cloud se utiliza principalmente para almacenar los datos y realizar consultas SQL**, mientras que el análisis exploratorio se desarrolla en Python mediante notebooks.

---

# 📁 Estructura del Proyecto

```
ecommerce-gcp-data-warehouse

│
├── data
│   ├── orders.csv
│   ├── order_items.csv
│   ├── customers.csv
│   └── products.csv
│
├── notebooks
│   └── ecommerce_analysis.ipynb
│
├── sql
│   └── data_warehouse_queries.sql
│
├── images
│   └── charts
│
└── README.md
```

---

# ⚙️ Procesamiento de Datos

El proyecto incluye varias etapas de procesamiento.

---

## 1️⃣ Ingesta de Datos

Los archivos CSV se cargan en:

🗄️ **Google Cloud Storage**

Este nivel funciona como un **Data Lake básico**, donde se almacenan los datos sin procesar.

---

## 2️⃣ Creación del Dataset en BigQuery

Los datos se importan a **BigQuery** para permitir consultas analíticas.

### Ejemplo de transformación SQL

```sql
CREATE OR REPLACE TABLE ecommerce_dw.fact_orders AS

SELECT
o.order_id,
o.customer_id,
oi.product_id,
o.order_purchase_timestamp,
oi.price,
oi.freight_value,
oi.price + oi.freight_value AS revenue

FROM ecommerce_dw.orders o
JOIN ecommerce_dw.order_items oi
ON o.order_id = oi.order_id;
```

---

## 3️⃣ Limpieza de Datos

Algunos pasos importantes de preparación incluyen:

* 🧹 eliminación de duplicados
* 🗓️ conversión de fechas
* 🔢 validación de valores numéricos
* 📊 creación de métricas derivadas

### Ejemplo en Python

```python
orders["order_purchase_timestamp"] = pd.to_datetime(
    orders["order_purchase_timestamp"],
    errors="coerce"
)
```

---

## 4️⃣ Feature Engineering

Se crearon nuevas variables para mejorar el análisis.

### Ejemplo

```python
items["revenue"] = items["price"] + items["freight_value"]
```

Esto permite calcular el **valor total de cada compra**.

---

# 🔎 Análisis Exploratorio de Datos

El proyecto analiza varias preguntas de negocio.

### 💰 Distribución de precios

Comprender cómo se distribuyen los precios de los productos.

### 🏆 Productos más vendidos

Identificar los productos con mayor volumen de ventas.

### 📦 Ingresos por categoría

Analizar qué categorías generan mayores ingresos.

### 📅 Tendencias mensuales de ventas

Examinar cómo cambian las ventas a lo largo del tiempo.

---

# 📊 Ejemplo de Visualización

Ejemplo de código utilizado para analizar ventas mensuales:

```python
monthly_sales = df.groupby("month")["revenue"].sum()

monthly_sales.plot(marker="o")
```

Este gráfico permite identificar **tendencias y estacionalidad en las ventas**.

---

# 💡 Principales Insights

Durante el análisis se encontraron varios hallazgos importantes:

* 🛍️ Un pequeño grupo de productos genera gran parte de los ingresos
* 📦 Algunas categorías destacan claramente sobre otras
* 🚚 Los costos de envío influyen significativamente en el valor final del pedido
* 📈 Las ventas muestran variaciones claras a lo largo del año

Estos resultados pueden ayudar a mejorar **estrategias de marketing y gestión de inventario**.

---

# 📊 Valor para el Negocio

Este tipo de análisis permite a las empresas:

* centralizar datos de e-commerce
* analizar grandes volúmenes de información
* identificar productos clave
* monitorear el rendimiento de ventas

Este flujo refleja el trabajo típico de un **Data Analyst que utiliza datos almacenados en la nube**.

