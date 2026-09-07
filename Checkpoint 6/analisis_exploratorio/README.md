# 📊 Proyecto de Análisis Exploratorio y Procesamiento de Datos (EDA & ETL)

¡Bienvenido! Este repositorio contiene un conjunto de herramientas y cuadernos de trabajo en **Python** diseñados para realizar procesos de extracción, transformación y carga (ETL), así como análisis exploratorio de datos (EDA) detallado. El proyecto aborda dos casos de estudio prácticos con datos reales: la **Incidencia Delictiva en México** (proveniente del Secretariado Ejecutivo del Sistema Nacional de Seguridad Pública - SESNSP) y una **Base de Datos de Películas de IMDB**.

---

## 🛠️ Tecnologías y Librerías

El análisis está construido sobre un stack moderno y eficiente de ciencia de datos en Python:

| Herramienta / Librería | Propósito |
| :--- | :--- |
| **Python 3.12+** | Entorno de ejecución principal |
| **Pandas** | Manipulación, filtrado, agrupamiento y reestructuración de dataframes |
| **NumPy** | Operaciones matemáticas y vectoriales optimizadas |
| **Matplotlib** | Graficación de bajo nivel y personalización de figuras |
| **Seaborn** | Visualizaciones estadísticas atractivas y avanzadas (heatmaps, distribuciones) |
| **JupyterLab** | Entorno interactivo para el desarrollo y documentación de código |
| **Chardet** | Detección automática del encoding en archivos de texto/CSV |

---

## 📁 Estructura del Proyecto

A continuación se detalla la organización de los archivos dentro del espacio de trabajo:

```text
analisis_exploratorio/
├── 1_limpieza_de_datos.ipynb      # Proceso de ETL para datos de incidencia delictiva
├── 2_eda_imdb.ipynb               # Análisis exploratorio detallado del dataset de IMDB
├── 3_ejercicios_pandas_delitos.ipynb # Consultas avanzadas y cálculo de tasas delictivas
├── requirements.txt               # Lista de dependencias del proyecto
├── LICENSE                        # Licencia del repositorio
├── data/                          # Almacenamiento de datasets (raw y procesados)
│   ├── datos_delitos.csv          # Dataset original de delitos del SESNSP (Wide format)
│   ├── delitos.csv                # Dataset limpio y transformado (Long format)
│   ├── imdb.csv                   # Base de datos de películas de IMDB
│   └── poblacion_entidades_2015.csv # Población de los estados para normalización de tasas
└── img/                           # Recursos gráficos y diagramas
    ├── datascientist_time.jpeg    # Ilustración sobre el tiempo invertido en limpieza
    ├── etl.png                    # Diagrama del proceso Extract, Transform, Load
    └── pandas_1.png               # Recursos adicionales de soporte visual
```

---

## 📓 Descripción de los Cuadernos de Trabajo

El proyecto está estructurado de manera secuencial para guiar al desarrollador en el flujo de trabajo estándar de un científico de datos.

### 🧹 1. Limpieza de Datos (ETL) — `1_limpieza_de_datos.ipynb`
Este notebook aborda la fase más crítica de cualquier proyecto de datos: **la preparación y limpieza**.
* **Detección de Encoding:** Solución de errores comunes de lectura (`UnicodeDecodeError`) mediante la herramienta `chardet` para identificar archivos codificados en `ISO-8859-1` o `latin1`.
* **Estandarización de Columnas:** Limpieza de nombres de columnas (conversión a minúsculas, reemplazo de espacios por guiones bajos y eliminación de caracteres especiales como acentos y la letra `ñ`).
* **Transformación a Formato Largo (Melt):** Reestructuración de la tabla original desde un formato ancho (donde cada mes era una columna independiente) a un **formato largo** (`long format`), ideal para el análisis de series de tiempo y agrupamientos estadísticos.
* **Procesamiento de Fechas:** Conversión de texto de meses a enteros mapeados, concatenación con el año y creación de una columna indexable de tipo `datetime`.
* **Exportación Final:** Generación del archivo unificado `data/delitos.csv`.

> [!NOTE]
> Este proceso convierte los datos originales en un formato estructurado y limpio, reduciendo significativamente la complejidad de las consultas posteriores.

---

### 🎬 2. Análisis Exploratorio de IMDB (EDA) — `2_eda_imdb.ipynb`
Estudio detallado del comportamiento de la industria del cine basándose en las películas mejor valoradas en IMDB.
* **Inspección Inicial:** Uso de `.head()`, `.tail()`, `.info()` y descriptores estadísticos para identificar tipos de datos y anomalías.
* **Tratamiento de Valores Nulos (NA):** Análisis del impacto de los valores faltantes en variables clave como `Metascore` y `Revenue (Millions)`, y su posterior limpieza.
* **Visualización de Distribuciones:** Creación de histogramas personalizados con Matplotlib y Seaborn para entender la distribución de las calificaciones (`Rating` y `Metascore`).
* **Estadística Descriptiva:** Cálculo de medidas de tendencia central utilizando Numpy y Pandas de manera comparativa.
* **Frecuencias y Visualización de Barras:** Agrupación y conteo de frecuencias por calificación, seguidos de gráficos de barras ordenados.
* **Matriz de Correlación:** Análisis multivariable para medir el coeficiente de correlación entre ingresos, calificación, votos y duración de las películas, graficado mediante mapas de calor (`matshow`).

---

### 🚨 3. Ejercicios Prácticos e Incidencia Delictiva — `3_ejercicios_pandas_delitos.ipynb`
Aplicación de consultas complejas y análisis estadísticos avanzados sobre los datos de delincuencia en México previamente procesados.
* **Series de Tiempo Multiestado:** Creación de un gráfico dinámico de series temporales de delincuencia para 3 estados de interés seleccionados (periodo de 2015-01 a 2019-07).
* **Resolución de Interrogantes de Negocio:**
  1. Homicidios totales registrados en una entidad específica (e.g., Colima) durante un año específico.
  2. Robos de vehículos automotores a nivel nacional.
  3. Suma combinada de delitos de alto impacto (homicidios y feminicidios) por año en toda la República.
  4. Entidad y mes con el máximo histórico de registros para delitos específicos (e.g., feminicidios).
* **Cálculo de Tasas Delictivas Normalizadas:** Integración cruzada (`merge`) del dataset de delitos con el archivo de población `poblacion_entidades_2015.csv`.
* **Cálculo de Tasa por cada 100,000 Habitantes:** Implementación de la fórmula matemática para obtener un indicador justo de criminalidad, permitiendo la comparación objetiva de incidencia entre estados con densidades poblacionales radicalmente opuestas (ejemplo: Estado de México vs. Colima).

---

## 🗃️ Diccionario de Datos

### `data/delitos.csv` (Procesado)
| Columna | Tipo de Dato | Descripción |
| :--- | :--- | :--- |
| `anio` | Entero | Año del registro del delito (2015 - presente) |
| `clave_ent` | Entero | Clave oficial de la entidad federativa según el INEGI |
| `entidad` | Texto | Nombre del estado de la República Mexicana |
| `tipo_de_delito` | Texto | Categoría principal del delito (e.g., Homicidio, Robo, Secuestro) |
| `nombre_mes` | Texto | Nombre del mes en minúsculas (enero, febrero, etc.) |
| `fecha` | Datetime | Fecha correspondiente al primer día del mes analizado (`YYYY-MM-DD`) |
| `frecuencia` | Entero | Cantidad de delitos registrados en dicho mes, estado y categoría |

---

## 🚀 Instalación y Guía de Uso

Sigue estos pasos para configurar tu entorno local y ejecutar los cuadernos de Jupyter:

### 1. Clonar el repositorio
Si tienes acceso vía Git, clona el proyecto en tu máquina local:
```bash
git clone <url_del_repositorio>
cd analisis_exploratorio
```

### 2. Crear un entorno virtual (Recomendado)
Es una buena práctica crear un entorno virtual para aislar las dependencias del proyecto:
* **En macOS y Linux:**
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```
* **En Windows:**
  ```bash
  python -m venv venv
  venv\Scripts\activate
  ```

### 3. Instalar las dependencias
Instala todas las librerías necesarias ejecutando el instalador de paquetes `pip` con el archivo `requirements.txt`:
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

---

## 📄 Licencia
Este proyecto se encuentra bajo la licencia **MIT**. Consulta el archivo [LICENSE](file:///Users/leonelmendiola/analisis_exploratorio/LICENSE) para obtener más detalles.
