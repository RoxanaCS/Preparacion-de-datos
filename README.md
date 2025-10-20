### Descripción

Este proyecto tiene como objetivo extraer, limpiar y unificar series de datos bancarios publicadas por el Banco Central de Chile. Los datos incluyen información sobre **colocaciones**, **captaciones** e **inversiones** de distintas instituciones financieras. El resultado final es un archivo CSV con los datos normalizados y listos para análisis financiero o estadístico.

---

### Tecnologías y Librerías

* **Python 3.9**
* Librerías:

  * `pandas` – manipulación y limpieza de datos
  * `numpy` – operaciones numéricas
  * `requests` – solicitudes HTTP
  * `BeautifulSoup` (`bs4`) – parseo de HTML
  * `re` – expresiones regulares

---

### Proceso Detallado

1. **Extracción de datos**

   * Se realiza un **web scraping** de la página del Banco Central de Chile para obtener los enlaces de descarga de archivos Excel (`.xlsx`).
   * Se descargan los archivos correspondientes a colocaciones, captaciones e inversiones.

2. **Lectura y unificación**

   * Se leen las hojas de cada archivo Excel.
   * Se eliminan filas y columnas irrelevantes.
   * Se renombra la columna de instituciones financieras y se despivotan los datos para un formato tabular uniforme.
   * Se agregan las columnas `Tipo`, `Subtipo` y `Moneda` según la información de cada hoja y archivo.

3. **Limpieza y normalización**

   * Eliminación de filas que no corresponden a bancos (`Total`, `ND`, etc.).
   * Normalización de la columna `Tipo`:

     ```
     sdbcol → colocación
     sdbdep → captación
     sdbinv → inversión
     ```
   * Conversión de la columna `Valor` a tipo numérico.
   * Ajuste de la columna `Moneda` eliminando la palabra "Saldo":

     ```
     Saldos en millones de pesos → millones de pesos
     Saldos en millones de dólares → millones de dólares
     ```
   * Reordenamiento de las columnas según lo solicitado:

     ```
     Fecha | Institución Financiera | Tipo | Subtipo | Valor | Moneda
     ```

4. **Archivo final**

   * Se genera un archivo CSV unificado llamado `sdbtotal_092021.csv` con todos los registros limpios y normalizados.

---

### Estructura del CSV Final

| Fecha      | Institución Financiera | Tipo       | Subtipo                                  | Valor     | Moneda            |
| ---------- | ---------------------- | ---------- | ---------------------------------------- | --------- | ----------------- |
| 2008-01-31 | Banco Bice             | colocación | Colocaciones totales por tipo de crédito | 1.763.607 | millones de pesos |
| 2008-01-31 | Banco Consorcio        | colocación | Colocaciones totales por tipo de crédito | 33.929    | millones de pesos |
| ...        | ...                    | ...        | ...                                      | ...       | ...               |

* **Filas finales:** 129,927
* **Columnas:** 6
* Datos listos para análisis estadístico, visualización o modelamiento financiero.

---

### Instrucciones de Instalación

1. Clonar el repositorio:

   ```bash
   git clone https://github.com/RoxanaCS/Preparacion-de-datos.git
   ```
2. Instalar dependencias:

   ```bash
   pip install pandas numpy requests beautifulsoup4
   ```

---

### Cómo ejecutar el proyecto

1. Ejecutar el script de Python:

   ```bash
   python script_preparacion_datos.py
   ```
2. El script descargará los archivos Excel, procesará los datos y generará el CSV final `sdbtotal_092021.csv`.
3. Abrir el CSV en Python, Excel o cualquier software de análisis de datos para explorar la información.

---

### Notas importantes

* Algunos valores en los Excel originales estaban marcados como `ND` (No existe dato) y se eliminan durante la limpieza.
* La columna `Tipo` indica si los datos corresponden a **colocación**, **captación** o **inversión**.
