---
title: "Descripción clínica de pacientes de la base de datos TCA-SKCM"
author: "Avila Aylén"
date: '2023'
output: html_document
---

<center> <h1> Trabajo Integrador</h1> </center>
<center> <h3>DIPLOMATURA EN VISUALIZACIÓN DE DATOS</h1> </center>
<center> <h4>FCEyE - UNR - AÑO 2023</h1> </center>


### Introducción
#### Cancer
<p style="text-align: justify;">El término cáncer incluye un gran grupo de enfermedades que afectan a diferentes partes del organismo caracterizadas por fallas en mecanismos
relacionados con la proliferación y diseminación celular. Durante el 2020 la mortalidad por cáncer ascendió a 10 millones de personas a nivel mundial (GLOBOCAN, 2020).</p>  
<p style="text-align: justify;">El desarrollo tumoral es un proceso complejo de múltiples pasos que puede culminar en una  transformación de células normales a malignas siendocaracterísticas la evasión del sistema inmune, resistencia a apoptosis y cambios morfológicos, entre otros.  
La metástasis consiste en la diseminación de las células cancerígenas desde su sitio de origen hacia otro órgano o tejido donde proliferan formando un nuevo tumor. Depende de propiedades tanto de la célula tumoral como de la persona huésped. El proceso metastásico es multifactorial y consiste en una compleja serie de pasos. La cascada metastásica es selectiva, parcialmente adaptativa, ineficiente y posee regulación genética y epigenética. El proceso de migración, desde el sitio tumoral de origen, puede ser por vía sanguínea, linfática o transcelómica y requiere que las células adquieran propiedades invasivas. Si bien no hay una única causa que conlleve a la desregulación del ciclo celular, proliferación celular y transición epitelio-mesénquima asociadas al desarrollo tumoral, hay ciertas familias de proteínas que controlan muchos procesos relacionados con estas funciones.</p>  

#### Melanoma
<p style="text-align: justify;"> Particularmente, el melanoma es originado por la transformación maligna y posterior proliferación descontrolada de los melanocitos, células derivadas embriológicamente de células madres pluripotentes de la cresta neural. Durante el desarrollo fetal, no sólo migran y se diferencian predominantemente dentro de la epidermis, sino también en otros sitios que contienen pigmentos extra cutáneos como los ojos, las meninges, el esófago y las membranas mucosas. Por lo tanto, se pueden caracterizar tres subtipos de melanoma: el melanoma cutáneo (el más común) que surge de los melanocitos en la epidermis, el melanoma mucoso y el melanoma uveal (Yousaf & Larkin, 2013). El melanoma cutáneo es la forma más severa del cáncer de piel y constituye un gran problema sanitario a nivel nacional y mundial. La incidencia global de melanoma continúa en aumento y los principales factores que predisponen a su desarrollo parecen estar relacionados con un aumento de exposición crónica a radiación UV (ASCO, 2019).</p>  

#### Características clínico-patológicas de interés
**Clínicas**
Se han seleccionado algunas características que han sido reportadas como interesantes para el análisis según la [American Cancer Society](https://www.cancer.org/es/cancer/tipos/cancer-de-piel-tipo-melanoma/acerca/estadisticas-clave.html).
- Sexo manifestado
- País en el que viven al momento del diagnóstico
- Edad al momento del diagnóstico
Puede resultar de interés identificar la variable sexo en conjunto con la edad ya que, en personas mayores a 50 años, los diagnosticos en mujeres  se han incrementado respecto de los de varones.  

**Patológicas**
El pronóstico y las opciones de tratamiento dependen de varios factores. A continuación se detallan alugnas características típicamente utilizadas para la estadificación tumoral:
- Sitio de extracción 
Se indica si el tejido de extracción corresponde a una metástasis lejana, al tumor primario, a un nodo linfático, etc. 
- Tipo tumoral
El melanoma puede ser un tumor primario o un tumor metastásico.
- Nivel de Clark
Es una característica _cualitativa_ de la profundidad de la diseminación del cáncer de piel. 
  - Clark I: solo se encuentra en la epidermis.
  - Clark II: comenzó a diseminarse a la dermis papilar (capa superior de la dermis). 
  - Clark III: se diseminó a través de la dermis papilar a la unión entre la dermis papilar y reticular (capa inferior de la dermis). 
  - Clark IV: diseminó a la dermis reticular. 
  - Clark V: diseminó al tejido subcutáneo.
- Ulceración
Se denomina ulceración a la ruptura de la piel que se encuentra sobre el melanoma. Es una característica _cualitativa_ dicotómica.
- Gosor de Breslow
Es una medida de la profundidad _cuantitativa_ del crecimiento del melanoma en la piel. Es utilizado, junto a otros indicadores, para determinar el estadio del cáncer. Se mide en milímetros  
- Estadío patológico
El estadio del melanoma surge de una combinación de las diferentes valoraciones a cada una de las categorías antes mencionadas. Es _cualitativo_ y  toma valores del 0 al IV.
#### Atlas genómico del cáncer (TCGA, The Cancer Genome Atlas)
<p style="text-align: justify;"> En 2006 y con el objetivo de recopilar y analizar datos clínicos y moleculares en distintos tipos tumorales, el National Cancer Institute junto al National Human Genome Research Institute crearon el consorcio [TCGA](https://portal.gdc.cancer.gov/) (TCGA, 2006). Este repositorio cuenta con datos clínicos, información histopatológica, datos genómicos, transcriptómicos, proteómicos y epigenéticos que se encuentran, en su gran mayoría, de libre acceso. Dentro de este repositorio se encuentran diferentes proyectos asociados a cada tipo de cáncer, para el caso del melanoma la denominación del proyecto es TCGA-SKCM (por sus siglas en inglés, Skin Cancer Cutaneous Melanoma).</p>

### R (CRAN: The Comprehensive R Archive Network)
<p style="text-align: justify;"> R es un lenguaje y un entorno diseñado para la implementación de técnicas y análisis estadísticos. Se trata de un lenguaje abierto y se encuentra disponible de manera gratuita, con una licencia GPL (general public license). Todas las variables, funciones, datos, salidas, operaciones (lógicas, comparativas, etc.), etc. son guardadas como objetos, por lo que R es un lenguaje orientado a objetos. Fue creado en 1993 por Ross Ihaka y Robert Gentleman en el Departamento de Estadística de la Universidad de Auckland, Nueva Zelanda. A partir de 1997 se conformó el equipo llamado “R Core Team” quienes tienen acceso a las modificaciones del código fuente. </p> 

**En este trabajo se propone acceder a la información clínica disponible en el proyecto TCGA-SKCM, utilizando el entorno R, para explorar y describir el set de datos.**

### Materiales y métodos
#### Librerías utilizadas
- RTCGA.clinical
```{r library RTCGA.clinical}
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("RTCGA")
library("RTCGA.clinical")
```
- Tidyverse
```{r library tidyverse}
install.packages("tidyverse")
library("tidyverse")
```
#### Acceso y limpieza del set de datos
- Descarga de datos
```{r clinica}
clinica<-as.data.frame(SKCM.clinical)
```
- Exploración de los datos disponibles
```{r clinica exploracion}
dim(clinica)
head(colnames(clinica))
```
- Selección, recodificación y reasignaciónde datos interesantes para este estudio
```{r datos}
datos<-clinica %>% 
  select(c(patient.age_at_initial_pathologic_diagnosis,
           patient.clinical_cqcf.country,
           patient.gender,
           patient.tumor_tissue_site,
           patient.clinical_cqcf.tumor_type,
           patient.melanoma_clark_level_value,
           patient.breslow_depth_value,
           patient.melanoma_ulceration_indicator,
           patient.stage_event.pathologic_stage))%>% 
  mutate(patient.stage_event.pathologic_stage = recode(patient.stage_event.pathologic_stage, 
                                                                       "i or ii nos"= "II",
                                                                       "stage 0"= "0",
                                                                       "stage i"= "I",
                                                                       "stage ia"= "I",
                                                                       "stage ib"= "I",
                                                                       "stage ii"= "II",
                                                                       "stage iia"= "II",
                                                                       "stage iib"= "II",
                                                                       "stage iic"= "II",
                                                                       "stage iii"= "III",
                                                                       "stage iiia"= "III",
                                                                       "stage iiib"= "III",
                                                                       "stage iiic"= "III",
                                                                       "stage iv"= "IV")) %>%
  mutate(patient.gender = recode(patient.gender,
                                 female= "Mujer",
                                 male= "Varón")) %>%
  mutate(patient.clinical_cqcf.tumor_type = recode(patient.clinical_cqcf.tumor_type,
                                          primary= "Primario",
                                          metastatic= "Metastasico")) %>%
  mutate(patient.tumor_tissue_site = recode(patient.tumor_tissue_site,
                                            "distant metastasis" = "Metástasis distante",
                                            "primary tumor"= "Tumor primario",
                                            "regional cutaneous or subcutaneous tissue (includes satellite and in-transit metastasis)"="Tejido regional",
                                            "regional lymph node"="Nodo linfático")) %>%
  mutate(patient.melanoma_ulceration_indicator = recode(patient.melanoma_ulceration_indicator,
                                                        yes = "Con",
                                                        no = "Sin"))%>%
  rename(Ulceracion=patient.melanoma_ulceration_indicator)%>%
  rename(Sitio_extraccion=patient.tumor_tissue_site)%>%
  rename(Pais=patient.clinical_cqcf.country)%>%
  rename(Tipo_tumoral=patient.clinical_cqcf.tumor_type)%>%
  rename(Sexo_manifestado=patient.gender)%>%
  rename(Estadio_tumoral=patient.stage_event.pathologic_stage)%>%
  rename(Edad=patient.age_at_initial_pathologic_diagnosis)%>%
  rename(Nivel_Clark=patient.melanoma_clark_level_value)%>%
  rename(Profundidad_Breslow=patient.breslow_depth_value)
datos[,c(1,7)]<-sapply(datos[,c(1,7)],as.numeric)
```
- Verificación de los datos seleccionados
```{r resumen}
summary(datos)
```
- Guardado de datos
```{r datos}
write.table(datos,"datos.txt")
```
### Resultados
La tabla con los datos seleccionados se encuentra disponible en el siguiente [link](https://github.com/ImoPupato/DiploVisDatos/blob/main/datos.txt).
#### Características de las personas incluidas en la base de datos
- Edad al momento del diagnóstico
```{r summary edad}
summary(datos$Edad)
```
- País de origen
```{r país}
table(na.omit(datos$Pais))
```
- Sexo manifestado
```{r sexo}
table(datos$Sexo)

```
#### características de los tumores
- Sitio de extracción tumoral
```{r sitio}
table(datos$Sitio_tumoral)
```
- Tipo tumoral
```{r tipo tumoral}
table(na.omit(datos$Tipo_tumoral))
```
- Nivel Clark
```{r clark}
table(na.omit(datos$Nivel_Clark))
```
- Profundidad de Breslow
```{r breslow} summary(na.omit(datos$Profundidad_Breslow))
```
- Ulceración
```{r ulceración} 
table(datos$Ulceracion)
```
- Estadío tumoral patológico
```{r estadio pat}
table(datos$Estadio_tumoral)
```

