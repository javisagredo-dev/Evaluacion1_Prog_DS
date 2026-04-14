# Proyecto de Análisis de Sismicidad en Chile

**Integrantes:**  
- Cristian Romero
- Javier Sagredo

## Origen y descripción de los datos

Los datos utilizados provienen de un archivo público (`archive.zip`) que contiene registros sísmicos globales desde el año 1900 hasta 2026. Incluye información como fecha, hora, coordenadas geográficas (latitud/longitud), profundidad, magnitud, tipo de magnitud (`magType`), y otras variables técnicas. El conjunto original tiene más de 1 millón de eventos.

Para este proyecto se filtraron únicamente los sismos ocurridos dentro del territorio chileno, incluyendo tanto la zona terrestre (regiones) como la Zona Económica Exclusiva (mar). Esto se realizó mediante unión de shapefiles de regiones y el polígono de la ZEE de Chile, reduciendo el dataset a ~39.600 eventos relevantes.

## Justificación del entorno (Google Colab)

Se optó por **Google Colab** por las siguientes razones:

- **Acceso a GPU gratuita** – útil para posibles modelos de machine learning.
- **Almacenamiento en la nube** – los datos y resultados se guardan directamente en Google Drive, evitando problemas de espacio local.
- **Colaboración en tiempo real** – permite trabajar simultáneamente con el compañero sin conflictos de versiones.
- **Sin configuración local** – no requiere instalar librerías ni gestionar entornos virtuales.
- **Integración sencilla con GitHub** – se puede abrir directamente un notebook desde un repositorio público, y los cambios pueden descargarse como `.ipynb` y subirse con `git commit`. Además, Colab ofrece un botón "Open in Colab" para que cualquier revisor pueda ejecutar el análisis sin preparación previa.

## Estructura del proyecto

- **Carga y filtrado espacial** – lectura del CSV, conversión a GeoDataFrame y filtro por polígonos de Chile.
- **Limpieza y selección de columnas** – eliminación de variables no útiles (nst, gap, dmin, rms, net, updated, status, geometry, etc.) y creación de nuevas columnas de fecha/hora.
- **Análisis exploratorio (EDA)** – visualización de mapa de calor con Folium, gráfico de barras por año, estadísticas descriptivas y segmentación por tipo de magnitud (`magType`).
- **Feature engineering y preprocesamiento** – escalado de variables numéricas (`latitude`, `longitude`, `depth`) con `StandardScaler`, y codificación one‑hot de `magType`.
- **Exportación** – el DataFrame limpio y filtrado se guarda en la carpeta `Processed/` del Google Drive como `sismos_chile.csv`.

## Resultados clave

- Solo el **3.76%** de los sismos globales ocurren en territorio chileno (incluyendo mar).
- La magnitud promedio es ~3.97, con un máximo de 9.5 (terremoto de Valdivia 1960).
- Las magnitudes de tipo `mw` (magnitud momento) son las más confiables para grandes terremotos.
- Se decidió **no eliminar outliers** de magnitud ni profundidad, ya que los eventos extremos son los más relevantes para el estudio de tsunamis y peligro sísmico.

## Cómo ejecutar el notebook

1. Abrir el archivo `Evaluacion_1_Prog_DS(2).ipynb` en Google Colab (botón "Open in Colab" al inicio del notebook).
2. Montar Google Drive cuando se solicite.
3. Asegurar que las rutas de los archivos (`archive.zip`, `REGIONES_v1.shp`, `eez.xml`) sean correctas en el Drive.
4. Ejecutar todas las celdas secuencialmente.

## Enlace al repositorio

[https://github.com/javisagredo-dev/Evaluacion1_Prog_DS](https://github.com/javisagredo-dev/Evaluacion1_Prog_DS)
