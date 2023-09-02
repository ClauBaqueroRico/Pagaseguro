
<center>

![UNIANDES Banner](figs/ans_banner_1920x200.png)

</center>


<center><h1>Transición hacia un modelo para la Industria de Seguros de Vehículos. 'Paga Según Manejas' – Grupo 5</h1></center>

## Resumen del proyecto

Cada vez un mercado más competitivo y complejo como el sector de seguros requiere una mayor innovación para mantener y mejorar cada vez más su participación en el mercado; por lo que se propone un nuevo método denominado "paga según manejas” para la clasificación de asegurados para una compañía de seguros en Bogotá, Colombia, basado en información de siniestralidad pública de la ciudad. El modelo incluye la incorporación de análisis de la información, con características categóricas, ordinales y numéricas comprendiendo desafíos adicionales a los modelos supervisados presentes en la actualidad. Propendiendo en superar el modelo actual de categorías de tarifas de seguros de automóviles, que depende principalmente de las características de los vehículos y sus propietarios lo que permitirá unas categorías de tarifas más precisas y justas que beneficien el buen comportamiento de los conductores mientras siguen siendo rentables y sostenibles para la compañía de acuerdo con las posibles anomalías presentes en las reclamaciones. Nuestra contribución clave será la identificación de patrones en accidentes viales y la categorización de asegurados según la información de accidentes del periodo. Para este desarrollo se implementan técnicas analíticas de clasificación de aprendizaje no supervisado, estimaciones de métricas y medidas de similitud de los accidentes analizados.


## Descripción de los datos utilizados en este proyecto

Se emplean los datos de https://www.movilidadbogota.gov.co/web/simur correspondiente a la consolidación de siniestros viales ocurridos durante el año 2019 en la ciudad de Bogotá, incluyendo información detallada de cada evento, ubicación geográfica, vehículos involucrados, información de conductores y caracterización de las víctimas.


## Archivos y estructura del repositorio

```
📦 MarketSegInsurancePayAsYouDrive
 ┣ 📄 Base_Accidentes.ipynb --> Notebook con el pre procesamiento y exploración de ACCIDENTES.
 ┣ 📄 Base_Conductores.ipynb --> Notebook con el pre procesamiento y exploración de CONDUCTORES.
 ┣ 📄 Base_Victimas.ipynb --> Notebook con el pre procesamiento y exploración de VICTIMAS.
 ┣ 📄 README.md --> Documento de orientación y explicación del proyecto y sus archivos.
 ┣ 📄 .gitignore --> Archivo para ignorar archivos y carpetas a versionar.
 ┣ 📂 data --> Carpeta con los datos a trabajar.
 ┃ ┣ 📄 Base_2019.xlsx --> Dataset original de la fuente.
 ┃ ┣ 📄 Base_2019_con_latitud_longitud.xlsx --> Dataset original complementado con latitudes y longitudes.
 ┃ ┗ 📄 Base_accidentes.xlsx --> Base de accidentes con imputaciones almacenadas (debido al tiempo que tomó el procesarla)
 ┣ 📂 docs --> Archivos de documentación y entregas.
 ┃ ┣ 📄 Anuario_Siniestralidad_2019.pdf --> Archivo de exploración que acompañaba la base original.
 ┃ ┣ 📄 E1 Proyecto.docx --> Entrega 1 del proyecto en word.
 ┃ ┗ 📄 E1 Proyecto.pdf --> Entrega 1 del proyecto en PDF.
 ┗ 📂 figs --> Imágenes de apoyo o recurso.
    ┗ 📄 ans_banner_1920x200.png --> Banner de UniAndes.
 ```


## Metodología

A grandes rasgos este proyecto se abordará bajo los siguientes pasos y premisas:

1. Preprocesamiento de Datos.
2. Exploración de los Datos.
3. Aplicación de algoritmos no supervisados en los Datos.
4. Evaluación y validación.
5. Conclusiones y recomendaciones. 


## Integrantes del equipo

Al ser un proyecto final de la materia Aprendizaje No Supervisado de la Univeridad de los Andes en el semestre 2023-2 se relacionan los integrantes miembros del equipo encargado de este proyecto:

* Claudia Marcela Baquero Rico
* Johan Alberto Medina Cetina
* Daniel Hoyos Ospina