# Telecom X - Análisis de Evasión de Clientes (Churn)

## Introducción

Este repositorio contiene el análisis de datos para el proyecto "Churn de Clientes" de la empresa Telecom X. La compañía enfrenta una alta tasa de cancelación de servicios y este análisis tiene como objetivo identificar los factores clave que contribuyen a la pérdida de clientes.

El objetivo principal es realizar un proceso completo de ETL (Extracción, Transformación y Carga) y un Análisis Exploratorio de Datos (EDA) para extraer insights valiosos. Estos hallazgos servirán como base para que el equipo de Ciencia de Datos pueda desarrollar modelos predictivos y estrategias efectivas para reducir la tasa de churn.

## Proceso ETL (Extract, Transform, Load)

### Extracción

Los datos fueron extraídos de una API en formato JSON. Se utilizó la biblioteca `pandas` de Python para cargar los datos directamente en un DataFrame, facilitando su manipulación y análisis.

### Transformación

La fase de transformación fue crucial para asegurar la calidad y consistencia de los datos. Los pasos realizados fueron:

1.  **Normalización de Datos:** Se desanidaron las columnas con datos estructurados (JSON anidado) como `customer`, `phone`, `internet` y `account` para convertir cada atributo en una columna individual.
2.  **Limpieza de Datos:**
    *   Se manejaron valores inconsistentes en la columna `Charges.Total`, donde algunos registros de clientes nuevos (antigüedad de 0 meses) tenían un espacio en blanco en lugar de un valor numérico. Estos fueron convertidos a 0.
    *   Se eliminaron filas donde la variable objetivo `Churn` no estaba definida (contenía un valor vacío).
    *   Se verificó la no existencia de registros duplicados.
3.  **Ingeniería de Características (Feature Engineering):**
    *   Se creó la columna `Cuentas_Diarias` a partir de la columna `Charges.Monthly` para obtener una perspectiva del gasto diario del cliente, asumiendo 30 días por mes.
4.  **Estandarización:** Se convirtieron las columnas categóricas con respuestas binarias (ej. '''Sí'''/'''No''') a un formato numérico (1/0) para facilitar el análisis cuantitativo y la futura implementación de modelos. Las columnas estandarizadas incluyen `Churn`, `Partner`, `Dependents`, `PhoneService` y `PaperlessBilling`.

## Análisis Exploratorio de Datos (EDA)

Se realizó un análisis exploratorio para comprender las características de los clientes y su relación con la tasa de cancelación. El análisis incluyó:

*   **Análisis Descriptivo:** Cálculo de métricas estadísticas (media, mediana, desviación estándar) para las variables numéricas.
*   **Visualización de Datos:** Creación de gráficos para analizar la distribución de la variable `Churn` y su relación con otras variables categóricas (género, tipo de contrato, método de pago) y numéricas (antigüedad, cargos mensuales y totales).

## Conclusiones e Insights

El análisis reveló patrones importantes sobre los clientes que tienen una mayor probabilidad de cancelar el servicio:
*   Los clientes con contratos de **mes a mes** tienen una tasa de cancelación significativamente más alta en comparación con los contratos anuales.
*   Los clientes que utilizan el pago mediante **cheque electrónico** son más propensos a cancelar.
*   La falta de servicios como **seguridad en línea (OnlineSecurity)** y **soporte técnico (TechSupport)** parece estar correlacionada con una mayor tasa de churn.
*   Los clientes más nuevos (con menor **antigüedad o tenure**) son más propensos a irse.

## Recomendaciones

Basado en los insights obtenidos, se proponen las siguientes recomendaciones estratégicas:

1.  **Fomentar Contratos a Largo Plazo:** Ofrecer incentivos y descuentos para que los clientes opten por contratos de uno o dos años.
2.  **Optimizar Métodos de Pago:** Analizar y mejorar la experiencia de pago con cheque electrónico o incentivar el uso de métodos de pago automáticos que tienen menor tasa de churn.
3.  **Paquetes de Servicios de Valor Agregado:** Promocionar y ofrecer descuentos en servicios de seguridad en línea y soporte técnico, especialmente para clientes nuevos.
4.  **Programas de Lealtad:** Implementar programas de fidelización para clientes que superen ciertos hitos de antigüedad en la empresa.

## Cómo ejecutar el proyecto

### Requisitos

*   Python 3.x
*   Jupyter Notebook o Google Colab
*   Bibliotecas de Python:
    *   pandas
    *   matplotlib
    *   seaborn

### Instrucciones

1.  Clonar el repositorio.
2.  Asegurarse de tener las bibliotecas necesarias instaladas:
    ```bash
    pip install pandas matplotlib seaborn
    ```
3.  Abrir el notebook `challenge2-data-science-LATAM-main/TelecomX_LATAM.ipynb` en Jupyter Notebook o Google Colab y ejecutar las celdas en orden.
