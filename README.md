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

### Conclusiones

Entre los años registrados en los datasets, 2016 a 2021, se registraron en total 695 siniestros viales, los cuales provocaron 716 víctimas fatales, de las cuales 544 fueron del sexo masculino (76.62%) y 166 del sexo femenino (23.38%). El grupo de edades de mayor riesgos fue entre los 25 y 45 años.

Los meses de Noviembre y Diciembre resultaron con el mayor número de siniestros en el período analizado. En relación al tipo de movilidad de las víctimas fatales en accidentes, el mayor riesgo lo tienen los motociclistas con un 42.04%, seguidos de los peatones con un 37.15% y en tercer lugar los conductores de autos que representaron el 12.85%.

Parte de las recomendaciones están enfocadas en aumentar el nivel de concientización en la población masculina de mediana edad, así como también reforzar las campañas durante los últimos meses del año que tienen mayor concentración de siniestros. También es sumamente importante concientizar sobre el riesgo que tienen los peatones por más que no estén usando un medio de transporte público o privado, y sobretodo a los motociclistas que son los principales afectados según la investigación.

### Tecnologías utilizadas

Para la realización del proyecto se utilizó Python, NumPy, Pandas, Matplotlib y Seaborn en un notebook de Google Colaboratory para desarrollar los procesos de Análisis Exploratorio de los Datos (EDA) y para la Extracción, Transformación y Carga de los mismos (ETL). La visualización de los análisis y resultados se realizó en un dashboard interactivo utilizando Power BI.

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white) ![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)  
![Matplotlib](https://img.shields.io/badge/Matplotlib-3776AB?style=for-the-badge&logo=matplotlib&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-013243?style=for-the-badge&logo=seaborn&logoColor=white) ![Excel](https://img.shields.io/badge/Microsoft%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)  ![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=white) 

### Autor
#### Pablo Juárez Brizzi

