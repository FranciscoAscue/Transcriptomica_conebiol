---
layout: page
title: Ejecucion de funciones y scripts en R
parent: Comandos y scritps Basicos
---

# Introducción a R con un enfoque bioinformático

## R y RStudio

### ¿Qué es R?
* R es un lenguaje de programación y un ambiente de cómputo estadístico
* R es software libre (no dice qué puedes o no hacer con el software), de código abierto (todo el código de R se puede inspeccionar - y se inspecciona).
* Cuando instalamos R, instala la base de R. Mucha de la funcionalidad adicional está en **paquetes** que la comunidad crea.

#### ¿Por qué R?
* R funciona en casi todas las plataformas (Mac, Windows, Linux).
* R es un lenguaje de programación completo, permite desarrollo de DSLs (funciones muy específicas)
* R promueve la investigación reproducible: no sólo de análisis sino de cómo se hicieron las figuras.
* R está actualizado gracias a que tiene una activa comunidad. Solo en CRAN hay cerca de 8000 paquetes (funcionalidad adicional de R creadas creada por la
comunidad).
* R se puede combinar con herramientas bioinformáticas y formatos de datos procesados (e.g. plink, vcf, etc) para realizar análisis y figuras.
* R tiene capacidades gráficas muy sofisticadas.
* R es popular como herramienta estadística (la guerra del software) y cada vez más también como herramienta bioinformática.
* Además del repositorio de paquetes de todo tipo de R (CRAN) también hay un repositorio especializado en paquetes de bioinformática (Bioconductor)


#### ¿Cómo entender R?
* Hay una sesión de R corriendo. La consola de R es la interfaz entre R y nosotros.
* En la sesión hay objetos. Todo en R es un objeto: vectores, tablas,  funciones, etc.
* Operamos aplicando funciones a los objetos y creando nuevos objetos.

##### La consola (o terminal)
Es una ventana que nos permite comunicarnos al motor de R. Esta ventana acepta **comandos** en el lenguaje de R y brinda una respuesta (resultado) a dichos comandos.

Por ejemplo, le podemos pedir a R que sume 1+1 así:

```
1+1
```    

La consola se distingue por tener el símbolo `>` seguido de un cursor parpadeante que espera a que le demos instrucciones (cuando recién abrimos R además muestra la versión que tenemos instalada y otra info).

Tu Consola debe verse más o menos así después del ejemplo anterior:

![Consola](http://sahirbhatnagar.com/EPIB607/inst/figures/RStudio_overview.PNG)


##### Scripts y el editor

Como hemos visto en otras unidades, un **script** es un archivo de nuestros análisis que es:

* un archivo de texto plano
* permanente,
* repetible,
* anotado y
* compartible


En otras palabras, un script es una recopilación por escrito de las instrucciones que queremos enviar a la consola, de modo que al tener esas instrucciones cualquiera pueda repetir el análisis tal cual se hizo.

Un script muy sencillo podría verse así:

![Script](https://bookdown.org/ndphillips/YaRrr/images/runningcode.png)


RStudio brinda además de la consola un editor de texto, que es la pantalla que se observa en el ejemplo anterior. Lo que escribas en el editor de texto puede "enviarse" a la consola con los shortcuts de abajo o con el ícono correr.

La idea es que en el editor de texto vayas escribiendo los comandos y comentarios de tu **script** hasta que haga exactamente lo que quieras.


## Funciones básicas de R más importantes para bioinformática

### R Básico
\
Antes de pasar a las funciones bionformáticas, veamos la sintaxis básica de R y los principales comandos que aprender.  

En resumen:

* Expresiones matemáticas: `1+1`
* Strings de texto: `"¡Holaaaaa mundo!"`
* Valores lógicos: `1<5`, `2+2 ==5`
* Crear una variable u **objeto**: `x<-5`

* Funciones: son un comando que hace algo específico dentro de R. 

A diferencia de bash, en R los comandos, o funciones, tienen la sintaxis: "nombre_de_la_funcion()". Entre los paréntesis van los **argumentos** de la función, es decir los datos o parámetros con los cuales queremos que la función haga algo. Para ver qué hace una función, podemos correr en la terminal `?nombre_de_la_funcion`, lo cual abrirá la ayuda detallando los argumentos y cualquier otra información e cómo usar dicha función.

Ejemplo de funciones: `sum()`, `mean()` , log().

Vamos a ver l ayuda de la función `log()` con `?log`.

![](https://github.com/u-genoma/BioinfinvRepro/raw/master/Unidad3/log_help.png)


Matrices

* Matrices `matrix(0, 3, 5)`
* Acceso a elementos e una matriz `[ , ]`

Data frames

* Data frame `data.frame(x = c("a", "b", "c"), y = 1:3)`
* Acceso a elementos e una data.frame `[ , ]`, `$`


### Cargar archivos:
`read.delim` sirve para cargar un archivo de texto con filas y columnas. Revisa su ayuda para determinar qué parámetros utilizar para leerlo si está separado por comas, tabulaciones (tab), espacios o qué.

Además de archivos de filas y columnas, se pueden leer a R todo tipo de archivos, en algunos casos esto se hace con paquetes que crearon funciones específicas para esto. Normalmente se llaman `read.algo`. Por ejemplo la función `read.plink` del paquete snpMatrix.

Cuando utilices `read.delim` o símil, asume que tu WD es donde vive tu script y **utiliza rutas relativas** para navegar hasta el archivo que deseas cargar.

#### Working directory
Buena práctica recomendada: que tu working directory sea donde sea que viva el script en el que estás trabajando.

Para averiguar cuál es tu WD actual utiliza `getwd()`.

Puedes definir tu WD manualmente con la función `setwd()`, pero OJO: realiza esto en **La Consola**, *NO en tu script*. 

Una trampa práctica en RStudio para que tu WD sea el lugar donde vive tu script es ir al Menú:

`Session > Set Working Directory > To source file location`

O sease "source file" = tu script activo.

Nota también que si abres RStudio clickeando su ícono, tu WD por default será el home de tu usuario. Sin embargo, si abres RStudio clickeando en un script, el WD default será donde viva dicho script.


### Trabajar con paquetes y datos externos

R base contiene las funciones más básicas, pero la verdadera riqueza de R está en sus paquetes. Estos los puede desarrolar cualquier persona y publicar. Van desde análisis estadísticos generales hasta funciones muy específicas pera determinado campo. En [CRAN](https://cran.r-project.org/) puedes explorar la gran gama de paquetes sobre cualquier tema. Algunos paquetes son especializados para bioinformática, como [adegenet](http://adegenet.r-forge.r-project.org/) y [ape](https://cran.r-project.org/web/packages/ape/ape.pdf). Puedes ver una lista de más paquetes relacionados con genética estadística en [CRAN Task Statistical Genetics](https://cran.r-project.org/web/views/Genetics.html).

Otra opción para encontrar paquetes útiles es googlear "R package" + keywords de tu tema de interés, por ejemplo "metabarcoding".

(También hay un repositorio especializado en paquetes de bioinformática (Bioconductor), que veremos más adelante)

`install.packages` sirve para instalar un paquete en nuestras máquinas, esto la baja de CRAN u otro servidor y lo instala en **nuestro R**, pero **no lo carga a la sesión activa**. Este paso hay que hacerlo **solo una vez**.

Una vez que el paquete está instalado, este NO estará cargado en el cerebro de R al menos que utilicemos `library(nombredelpaquete)`. Este paso hay que hacerlo **cada vez que corras R para un análisis que ocupe dichos paquetes**.


Si tu script utiliza un paquete determinado, es recomendable que estos se carguen en las primeras líneas o al principio de la sección de código que los utilizará. Sólo carga los paquetes que realmente utilices en un script dado.

##### Cómo citar R 

Citar R:

```
citation("base")
```

Citar un paquete en particular:

```
citation("NombrePaquete")
```
(o lo que los autoreas especifiquen en su sitio web)


##### Funciones útiles al trabajar con paquetes y archivos de datos

* Funciones de sistema: `list.files`, `getwd`, `setwd`
* Cargar una función: `source`
* Instalar paquetes (sola una vez en cada equipo): `install.packages`.
* Cargar un paquete previamente instalado (cada vez que corramos el script): `library`.
* Cargar a R un archivo de texto con filas y columnas (separado por tabs o comas): `read.delim`.
* "Pegar" texto uno detrás de otro: `paste()` y `paste0()`.



### For loops

Al igual que en bash, en R pueden hacerse for loops, con la siguiente sintaxis:

`for (counter in vector) {commands}`

Ejemplo:

```{r}
for (i in 2:10){
  print(paste(i, "elefantes se columpiaban sobre la tela de una araña"))
}

```

La anterior es la versión más simple de un loop. Para otras opciones (como `while`, `if`, `if else`, `next`) revisa este [tutorial](https://www.datacamp.com/community/tutorials/tutorial-on-loops-in-r).

Los loops son útiles ya que nos permiten reciclar código en vez de repetir lo mismo para difernetes valores. Por ejemplo el loop anterior hace lo mismo que:

```{r}
paste(2, "elefantes se columpiaban sobre la tela de una araña")
paste(3, "elefantes se columpiaban sobre la tela de una araña")
paste(4, "elefantes se columpiaban sobre la tela de una araña")
paste(5, "elefantes se columpiaban sobre la tela de una araña")
paste(6, "elefantes se columpiaban sobre la tela de una araña")
paste(7, "elefantes se columpiaban sobre la tela de una araña")
paste(8, "elefantes se columpiaban sobre la tela de una araña")
paste(9, "elefantes se columpiaban sobre la tela de una araña")
paste(10, "elefantes se columpiaban sobre la tela de una araña")

```



```{r}
elefantes<-character(0)
for (i in 2:10){
  elefantes<-rbind(elefantes, (paste(i, "elefantes se columpiaban sobre la tela de una araña")))
}
elefantes

```



## Funciones propias: crear funciones y utilizarlas con source
 
`source` es una función que sirve para correr un script de R **dentro de otro script de R**. Esto permite modularizar un análisis y luego correr una pipeline general, así como tener por separado **funciones propias** (que podemos llamar igual que llamamos las funciones de los paquetes) y que utilizamos mucho en diversos scripts. Este tipo de funciones son las que podemos compartir en Github con otros usuarios y hasta convertirlas en un paquete.

Ejemplos de cómo utilizar `source`: correr el script del ejercicio anterior desde otro script con la línea.

```{r}
source("1.IBR_testing.r")
```
Nota que pare que esto funcione tu working directory debe ser el correcto para leer `1.IBR_testing.r` como si fuera un archivo (que lo es). Es decir tu WD debe ser la ruta donde está 1.IBR_testing.r (`Unidad3/PracUni3/mantel/bin/1.IBR_testing.r`)

**Hacer una función propia**:

Este es el [esqueleto de una función escrita dentro de R](http://www.statmethods.net/management/userfunctions.html):

```{r}
myfunction <- function(arg1, arg2, ... ){
statements
return(object)
}
```
**Ojo**: el comando `return` es necesario al final de una función siempre que queramos que dicha función "devuelva" un objeto (por ejemplo una df que creemos como parte de la función). De no poner esta instrucción, la función correrá desde otro script, pero no veremos ningún resultado.


Ejemplo:

```{r}
give_i_line<- function(file, i){
  ## Arguments
  # file = path to desired file with the indicadores, must be tab delimited and do NOT have a header
  # i = number of line of file we want to print

  ## Function
  # read indicadores list
  indicador<-read.delim(file, header=FALSE, quote="", stringsAsFactors=FALSE)

  # give text of the i line of the file  
  x<-indicador[i,1]
  return(x)
}

give_i_line("../data/indicadores.txt", i=2)
x<-give_i_line("../data/indicadores.txt", i=2)

```


Como alternativa a `return()` puedes poner el nombre del objeto (como si quisieras verlo en la terminal).


```{r}
give_i_line<- function(file, i){
  ## Arguments
  # file = path to desired file with the indicadores, must be tab delimited and do NOT have a header
  # i = number of line of file we want to print

  ## Function
  # read indicadores list
  indicador<-read.delim(file, header=FALSE, quote="", stringsAsFactors=FALSE)

  # give text of the i line of the file  
  x<-indicador[i,1]
  x
}

give_i_line("../data/indicadores.txt", i=2)
x<-give_i_line("../data/indicadores.txt", i=2)


```

Si quieres ver un resultado pero que este no sea guardado como un objeto, utiliza `print()`.

```{r}
give_i_line<- function(file, i){
  ## Arguments
  # file = path to desired file with the indicadores, must be tab delimited and do NOT have a header
  # i = number of line of file we want to print

  ## Function
  # read indicadores list
  indicador<-read.delim(file, header=FALSE, quote="", stringsAsFactors=FALSE)

  print(i)

  # give text of the i line of the file  
  x<-indicador[i,1]
  x
}

give_i_line("../data/indicadores.txt", i=2)
x<-give_i_line("../data/indicadores.txt", i=2)


```

Si guardamos la función como un script llamado [`give_i_line.r`](Prac_Uni3/ejemplosgenerales/bingive_i_line.r) después podemos correrla desde otro script, llamándola con `source()`:

```{r}
source("give_i_line.r")
give_i_line("../data/indicadores.txt"), i=2)
```

Nota que `source` NO corre la función en sí, sino que solo la carga al cerebro de R para que podamos usarla como a una función cualquiera de un paquete.

El nombre del archivo R no improta, pero es buena práctica ponerle el mismo que el nombre de la función.

## Rmarkdown y R Notebook

[R Markdown](http://rmarkdown.rstudio.com/index.html) es un formato que te permite crear documentos o reportes, en los que al mismo tiempo guardas y ejecutas código.

![alt text](https://github.com/u-genoma/BioinfinvRepro/raw/master/Unidad3/Rmarkdown1.png)

Primero, instala R Markdown:

```
 install.packages("rmarkdown")
```

Ahora puedes crear un archivo `.Rmd` en "Archivo > Nuevo archivo > R Markdown". (nota que esto es distinto que R script).

Un archivo R Markdown es un archivo de texto plano que debe verse algo así:

![alt text](https://github.com/u-genoma/BioinfinvRepro/raw/master/Unidad3/Rmarkdown_text.png)

El archivo tiene tres tipos de contenido:

- Encabezado (---)
- Código (```)
- Texto simple (Markdown)


Notarás que se pueden ejecutar las líneas de código de forma independiente e interactiva, y que el output (lo que saldría en la consola o los plots) del código de muestra debajo de éste.


Cuando abres o creas un archivo Rmd la interfaz de RStudio cambia. Ahora, puedes ejecutar el código usando las flechas y los resultados se despliegan a continuación del código.

![alt text](https://github.com/u-genoma/BioinfinvRepro/raw/master/Unidad3/Notebook_interface.png)



**Archivos de salida**

A partir de un archivo .Rmd, es posible crear archivos de salida en una gran variedad de formatos, por ejemplo:

- HTML
- Documentos interactivos
- Word
- Diapositivas
- PDF
- Páginas web
- R Notebooks

Checa más formatos de salida [aquí](http://rmarkdown.rstudio.com/formats.html)

Para crear el reporte o archivo de salida, debes correr `render()`, dar click en "Knit" o ⇧+Ctrl+K.

Cuando se renderea un archivo .Rmd, también se crea un archivo html. Este es un archivo HTML que contiene el código y los output resultantes, que puede abrirse en cualquier explorador web y en RStudio.


 
## Manipulación y limpieza de datos en R

`dplyr` es un paquete super útil para hacer operaciones de transformación de datos. Vamos a ver su [Data Transformation Cheat Sheet](https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf) para aprender sus comandos principales.

Puedes ver más acordenos parecidos en [este link](https://www.rstudio.com/resources/cheatsheets/)




La manipulación y la limpieza da datos muchas veces es necesaria antes de poner hacer análisis en R. 

## Bioconductor

Como hemos visto los paquetes son un grupo de funciones que alguien desarrolla en torno a un tema específico. Muchos paquetes viven en CRAN. Pero también hay otros repositorios más especializados. **Bioconductor** es un repositorio de paquetes de R especializaos en en análisis de datos genómicos y de secuenciación masiva. Es decir, en Bioconductor encontrarás paquetes que NO están en CRAN.

![logo_bioconductor.gif](https://github.com/u-genoma/BioinfinvRepro/raw/master/Unidad3/logo_bioconductor.gif)

### Generalidades de Bioconductor

#### [Página principal de Bioconductor](https://www.bioconductor.org/)

#### [Paquetes de Bioconductor](https://www.bioconductor.org/packages/release/BiocViews.html#___Software)

Como los paquetes de Bioconductor están escritos en el lenguaje de R, muchos tendrán tipos de objetos particulares al paquete y funciones nuevas, pero con tener las bases de R que hemos visto estarás list@ para aprenderlo.

La mejor manera de conocer qué hace y  usar un paquete es seguir un tutorial o vignette.

Por ejemplo esta de [ggtree](https://www.bioconductor.org/packages/release/bioc/vignettes/ggtree/inst/doc/ggtree.html)  y esta de [SNPRelate](http://corearray.sourceforge.net/tutorials/SNPRelate/).

Además, BioConductor desarrolló una clase de objetos, llamados `GRanges` que permite almacenar y manipular intervalos genómicos y variables definidas a lo largo de un genoma. Los `GRanges` son particularmente útiles para representar y analizar anotaciones genómicas y alineamientos y son la base de varios paquetes de Bioconductor

Los `GRanges` están definidos en el paquete  [GenomicRanges](https://bioconductor.org/packages/release/bioc/html/GenomicRanges.html). Este [tutorial](https://bioconductor.org/packages/release/bioc/vignettes/GenomicRanges/inst/doc/GenomicRangesIntroduction.pdf) explica su funcionamiento básico y lo recomiendo mucho. También está bueno el Capítulo 9 *Working with Range Data* del libro de Vince Buffalo *Bioinformatics Data Skills*.


#### [Workflows](https://www.bioconductor.org/packages/release/BiocViews.html#___Workflow)

Para algunas tareas comunes en análisis genéticos, como [Variant calling](https://www.bioconductor.org/help/course-materials/2014/BioC2014/Lawrence_Tutorial.pdf).


#### Cursos y conferencias de Bioconductor

Hay muchos [cursos y conferencias](https://www.bioconductor.org/help/course-materials) sobre Bioconductor que ocurren anualmente y que van de temas generales a especializados en algún proceso. Para una intro general yo recomiendo el curso online [Bioconductor for Genomic Data Science](http://kasperdanielhansen.github.io/genbioconductor/) de Kasper D. Hansen que incluye videos y código con notas en R y html.

En el 2018, por primera vez en Latinamérica, se dió un curso de nivel intermedio-avanzado: [Latin American R/BioConductor Developers Workshop 2018](http://www.comunidadbioinfo.org/r-bioconductor-developers-workshop-2018/). Estén atentxs para nuevas ediciones.

#### Instalar Bioconductor y sus paquetes

1) Tener instalado R

2) Instalar bioconductor (`source` al script `biocLite.R` que nos permitirá instalar paquetes de Bioconductor).

```
source("https://bioconductor.org/biocLite.R")
biocLite()
```
(Si lo anterior manda algún error intenta http:// en vez de  https://)

3) Utilizar la función `biocLite` para instalar los paquetes deseados. Ejemplo:

```
biocLite("ggtree")
```

Nota: algunos paquetes necesitan pasos extra de instalación, como jalar algo de GitHub, pero esto será indicado en la documentación del paquete.

#### Cómo citar R y Bioconductor

Citar R:

```
citation("base")
```

Citar Bioconductor:

```
citation("Biobase")
```

Citar un paquete en particular:

```
citation("NombrePaquete")
```
(o lo que loas autoreas especifiquen en su sitio web)



## Primeros auxilios cuando algo no te corre en R


* Te falta una `,`
* Te sobra un espacio
* Cierra tus `()`
* El texto va entre `" "`
* Si no pusiste `<-` no has creado el objeto
* No estás donde crees que estás (encuéntrate con `getwd()`)


## Cargar paquetes de R. 

`ape` (leer archivos gff)  
paletas de colores `(viridis)`

```r
library(ape)
library(viridisLite)
library(viridis)
```

## Explorar nuestro genoma S. cerevisiae a partir de gff (archivo de anotacion)

```r
## Cargar gff file

gff_file <- read.gff("sequence.gff3", na.strings = c(".","?"), GFF3 = TRUE)
```

## Algunas estadisticas

```r
tab <- as.matrix(table(gff_file$type))

rnames <- as.matrix(rownames(tab))

etiquetas <- paste0(rnames[c(4,7,10,16),],"=",round(100 * tab[c(4,7,10,16),]/sum(tab[c(4,7,10,16),]), 2), "%")                                                       
par(mfrow=c(1,2), adj = TRUE)

pie(tab[c(4,7,10,16),], labels = etiquetas, col = viridis(4))

#pie(tab[c(4,7,10,16),], col = viridis(4), labels = paste0(tab[c(4,7,10,16),], "%"))

barplot(tab[c(4,7,10,16),], col = viridis(4), width = 60)

```