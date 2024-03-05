## Proyecto Data Analitycs (Individual 2)
### Contexto de Trabajo
El Observatorio de Movilidad y Seguridad Vial (OMSV), centro de estudios que se encuentra bajo la órbita de la Secretaría de Transporte del Gobierno de la Ciudad Autónoma de Buenos Aires, solicita la elaboración de un proyecto de análisis de datos, con el fin de generar información que le permita a las autoridades locales tomar medidas para disminuir la cantidad de víctimas fatales de los siniestros viales.

En Argentina, aproximadamente 4.000 personas fallecen cada año en accidentes de tráfico. A pesar de los esfuerzos realizados en muchas jurisdicciones para reducir la cantidad de estos incidentes, siguen siendo la principal causa de muertes violentas en el país. Según los informes del Sistema Nacional de Información Criminal (SNIC) del Ministerio de Seguridad de la Nación, entre 2018 y 2022 se registraron 19.630 muertes en siniestros viales en todo el país. Estas cifras equivalen a un promedio de 11 víctimas fatales diarias debido a accidentes de tráfico.

### Datasets
Los archivos para iniciar el trabajo se descargaron de la página [Buenos Aires Data](https://data.buenosaires.gob.ar/dataset/) son de uso público y se encuentran en formato Excel:

- Homicidios (XLSX): Información sobre homicidios en siniestros viales ocurridos en la Ciudad desde el año 2016 hasta el 2021. Los datos incluyen fecha y ubicación del hecho y tipo de transporte involucrado.

- Lesiones (XLSX): Información sobre las lesiones en siniestros viales ocurridos en la Ciudad desde el año 2019 hasta el 2021. Los datos incluyen fecha y ubicación del hecho y tipo de transporte involucrado.

### EDA y ETL

- [ETL](https://github.com/paulusbrizzi/BA-Siniestros-Viales/blob/main/notebooks/1_ETL.ipynb): Aquí se interpretaron los archivos a través de DataFrames de Pandas, mediante el parámetro sheet_name se pudieron recorrer cada una de las páginas del archivo .xlsx para poder cruzar la información que había en cada uno y asociarlas a distintas variables para generar distintos dataframes que luego serían integrados en uno solo.
Se exploró el tamaño del df, se normalizaron las variables a minúsculas para facilitar el tipeo, se vieron y cambiaron los tipos de datos de cada columna, se normalizaron los títulos modificados por la función pd.merge. También se agregaron los días de la semana para cada fecha y se integró una lista de barrios según la comuna de cada fila. También se chequearon nulos y duplicados.

- [EDA](https://github.com/paulusbrizzi/BA-Siniestros-Viales/blob/main/notebooks/2_EDA.ipynb): Se realizó primeras aproximaciones a los datos numéricos con .describe() para las variables numéricas. Se buscaron duplicados sin obtener ninguno.
Se buscaron outliers para diferentes variables numéricas, siendo la de n_victimas (número de víctimas) la única variable que los tenía (estos son 2 y 3).
Se realizó un mapa de correlación de variables y se pudo ver cierta correlación positiva entre edad de la víctima y hora de ocurrencia del siniestro.

![](https://raw.githubusercontent.com/paulusbrizzi/BA-Siniestros-Viales/main/img/1.png)

Se descubrió que la gran mayoría de los casos concentran 1 víctima, como indicaba el análisis de outliers.
También se pudo encontrar una concentración de edades entre los 25 y 60 años aproximadamente. Con una media de 38 aproximadamente. En el histograma de edades podemos ver cómo la mayor concentración se da en menores a 30 años.

![](https://raw.githubusercontent.com/paulusbrizzi/BA-Siniestros-Viales/main/img/2.png)

Luego se corrió un scatterplot para conocer la relación entre edad-hora-sexo. Destaca una concentración de víctimas masculino entre las 3 y 10 de la mañana, entre los 20 y 40 años de edad.

![](https://raw.githubusercontent.com/paulusbrizzi/BA-Siniestros-Viales/main/img/3.png)

Se conocieron edades de las víctimas según el año de ocurrencia. Así como el sexo de las víctimas (mayoritariamente masculinos), como también histogramas que muestran la distribución de edad según sexo de las víctimas.
También se realizaron histogramas para conocer el sexo y el medio de la víctima al momento del siniestro y aquí pudimos ver la gran participación de motociclistas masculinos y peatones de ambos sexos.

Por último se navegaron las variables relativas al desarrollo en el tiempo y se descubrió la ocurrencia de estos estos mayoritariamente durante los días Domingo, Sábado y Lunes.

En tanto a geografía, pudimos ver que los siniestros siguen teniendo una concentración en el centro de la ciudad (Comuna 1) así como en las comunas lindantes al río Riachuelo. También conocimos que las Avenidas son el hecho más común para los siniestros.

### Script Python en Power BI
![](https://github.com/paulusbrizzi/BA-Siniestros-Viales/blob/main/img/geopandas_distribuciongeografica.png?raw=true)

Se aplicó el siguiente gráfico en la presentación para facilitar la visualización de la distribución geográfica de todos los siniestros distribuidos en el Dataset.
De la misma manera, podemos observar cómo la mayoría de estos se concentra en la Comuna 1, en el centro de la ciudad (región Este y Sur).

### KPIs
![](https://github.com/paulusbrizzi/BA-Siniestros-Viales/blob/main/img/kpis.png?raw=true)
Se desarrollaron 3 KPIs:

1. Relacionado a cumplir el objetivo de lograr la reducción de la tasa de homicidio en un 10% (porcentaje de homicidios sobre las población total) de acuerdo al semestre anterior a analizar.
2. La reducción de la tasa de homicidios en un 7% anual para víctimas que conducían o viajaban en moto.
3. Se propuso la reducción de la tasa de homicidios en un 7% semestral de las víctimas peatones.

Estos dos últimos (motos y peatones) son dos factores altamente relacionados por su alto nivel de mortalidad a comparación de otros actores.

### Conclusiones

Los meses de Noviembre y Diciembre resultaron con el mayor número de siniestros en el período analizado. En relación al tipo de movilidad de las víctimas fatales en accidentes, el mayor riesgo lo tienen los motociclistas con un 42.04%, seguidos de los peatones con un 37.15% y en tercer lugar los conductores de autos que representaron el 12.85%.

Gracias a la distribución Scatterplot del EDA, pudimos observar cómo existe una concentración de víctimas fatales entre las 4 y 10 horas de la mañana especialmente durante los fines de semana. Además, que la gran mayoría de estas víctimas en este punto eran jóvenes masculinos entre 20 y 40 años aproximadamente.

Alternativamente, podemos concebir una concentración sobre el centro de la ciudad (región Este del territorio), sobre la Comunas 1, seguido de todas las lindantes al río Riachuelo y parte de la región Sur, entre estas las comunas 4, 8 y 9.

### Resoluciones - Recomendaciones
1. Enfocarse en los tipos de víctimas más vulnerables:
   - Motociclistas: Implementar campañas de concienciación a jovenes motociclistas sobre la seguridad vial para este grupo, incluyendo el uso obligatorio de cascos y equipamiento adecuado.
   - Peatones: Mejorar la infraestructura vial para la seguridad de peatones pensando en el adulto mayor, como la construcción de aceras, pasos de peatones y ciclovías.
2. Reducir la velocidad en zonas de alto riesgo:
   - Implementar en vias de alto riesgo en las avenidas medidas de control de velocidad como reductores de velocidad, radares y mayor presencia policial.
3. Recopilación y análisis de datos:
   - Implementar un sistema de recopilación de datos más robusto y preciso sobre accidentes de tránsito, incluyendo información sobre las causas, las víctimas y las condiciones ambientales.
   - Utilizar el análisis de datos para identificar patrones y factores de riesgo en los accidentes de tránsito.
4. Campañas de concienciación vial:
   - Implementar campañas de concienciación vial dirigidas a toda la población, en especial a las comunas 1, 4, 9 y 8, incluyendo conductores, motociclistas, peatones y ciclistas.
   - Enfatizar la importancia de la responsabilidad individual en la seguridad vial.

### Tecnologías utilizadas

Para la realización del proyecto se utilizó Python, NumPy, Pandas, Matplotlib y Seaborn en un notebook de Google Colaboratory para desarrollar los procesos de Análisis Exploratorio de los Datos (EDA) y para la Extracción, Transformación y Carga de los mismos (ETL). La visualización de los análisis y resultados se realizó en un dashboard interactivo utilizando Power BI.

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white) ![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)  
![Matplotlib](https://img.shields.io/badge/Matplotlib-3776AB?style=for-the-badge&logo=matplotlib&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-013243?style=for-the-badge&logo=seaborn&logoColor=white) ![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)  ![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=white) 

### Autor
#### Pablo Juárez Brizzi

