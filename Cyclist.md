# Cyclist
#### Felipe Vergara
#### 2023-08-18
# Informe R Cyclist
### Instalar paquetes
install.packages("tidyverse", repos = "https://cran.rstudio.com/")

\## Installing package into 'C:/Users/felip/AppData/Local/R/win-library/4.3'

\## (as 'lib' is unspecified)

\## package 'tidyverse' successfully unpacked and MD5 sums checked

\## 

\## The downloaded binary packages are in

\##  C:\Users\felip\AppData\Local\Temp\RtmpQzLoGP\downloaded\_packages

install.packages("lubridate", repos = "https://cran.rstudio.com/")

\## Installing package into 'C:/Users/felip/AppData/Local/R/win-library/4.3'

\## (as 'lib' is unspecified)

\## package 'lubridate' successfully unpacked and MD5 sums checked

\## 

\## The downloaded binary packages are in

\##  C:\Users\felip\AppData\Local\Temp\RtmpQzLoGP\downloaded\_packages

install.packages("ggplot2", repos = "https://cran.rstudio.com/")

\## Installing package into 'C:/Users/felip/AppData/Local/R/win-library/4.3'

\## (as 'lib' is unspecified)

\## package 'ggplot2' successfully unpacked and MD5 sums checked

\## 

\## The downloaded binary packages are in

\##  C:\Users\felip\AppData\Local\Temp\RtmpQzLoGP\downloaded\_packages

install.packages("scales", repos = "https://cran.rstudio.com/")

\## Installing package into 'C:/Users/felip/AppData/Local/R/win-library/4.3'

\## (as 'lib' is unspecified)

\## package 'scales' successfully unpacked and MD5 sums checked

\## 

\## The downloaded binary packages are in

\##  C:\Users\felip\AppData\Local\Temp\RtmpQzLoGP\downloaded\_packages
### Cargar librerias
library(scales)

library(ggplot2)

library(tidyverse)

\## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──

\## ✔ dplyr     1.1.2     ✔ readr     2.1.4

\## ✔ forcats   1.0.0     ✔ stringr   1.5.0

\## ✔ lubridate 1.9.2     ✔ tibble    3.2.1

\## ✔ purrr     1.0.1     ✔ tidyr     1.3.0

\## ── Conflicts ────────────────────────────────────────── tidyverse\_conflicts() ──

\## ✖ readr::col\_factor() masks scales::col\_factor()

\## ✖ purrr::discard()    masks scales::discard()

\## ✖ dplyr::filter()     masks stats::filter()

\## ✖ dplyr::lag()        masks stats::lag()

\## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

library(dplyr)

library(geosphere)

\## The legacy packages maptools, rgdal, and rgeos, underpinning the sp package,

\## which was just loaded, will retire in October 2023.

\## Please refer to R-spatial evolution reports for details, especially

\## https://r-spatial.org/r/2023/05/15/evolution4.html.

\## It may be desirable to make the sf package available;

\## package maintainers should consider adding sf to Suggests:.

\## The sp package is now running under evolution status 2

\##      (status 2 uses the sf package in place of rgdal)
## Importación de datos
### Lectura y combinación de archivos CSV
setwd("C:/Users/felip/OneDrive/Documentos/R/Cyclistic/")

current\_directory <- getwd()

print(current\_directory)

\## [1] "C:/Users/felip/OneDrive/Documentos/R/Cyclistic"

file\_names <- c("202306-divvy-tripdata.csv","202305-divvy-tripdata.csv","202304-divvy-tripdata.csv","202303-divvy-tripdata.csv",

`                `"202302-divvy-tripdata.csv","202301-divvy-tripdata.csv","202212-divvy-tripdata.csv","202211-divvy-tripdata.csv",

`                `"202210-divvy-tripdata.csv","202209-divvy-tripdata.csv","202208-divvy-tripdata.csv","202207-divvy-tripdata.csv"

`                `)

combined\_data <-data.frame()

for (file in file\_names) {

`  `file\_data <- read\_csv(file)

`  `combined\_data<- rbind(combined\_data,file\_data)

}

\## Rows: 719618 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 604827 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 426590 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 258678 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 190445 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 190301 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 181806 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 337735 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 558685 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 701339 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 785932 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

\## Rows: 823488 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.

write.csv(combined\_data,"C:/Users/felip/OneDrive/Documentos/R/Cyclistic/Total\_Cycling\_data.csv", row.names = FALSE)
### LLamar el documento y guardarlo en una variable
Total\_data <- read\_csv("C:/Users/felip/OneDrive/Documentos/R/Cyclistic/Total\_Cycling\_data.csv")

\## Rows: 5779444 Columns: 13

\## ── Column specification ────────────────────────────────────────────────────────

\## Delimiter: ","

\## chr  (7): ride\_id, rideable\_type, start\_station\_name, start\_station\_id, end\_...

\## dbl  (4): start\_lat, start\_lng, end\_lat, end\_lng

\## dttm (2): started\_at, ended\_at

\## 

\## ℹ Use `spec()` to retrieve the full column specification for this data.

\## ℹ Specify the column types or set `show\_col\_types = FALSE` to quiet this message.
## Limpieza de datos
### Liempieza de datos y almacenar en una nueva variable
clean\_Total\_data<- Total\_data %>% 

`  `na.omit() %>% 

`  `unique() %>% 

`  `mutate(across(everything(), ~trimws(.))) %>% 

`  `mutate(

`    `start\_lat = round(as.numeric(start\_lat), 2),

`    `start\_lng = round(as.numeric(start\_lng), 2),

`    `end\_lat = round(as.numeric(end\_lat), 2),

`    `end\_lng = round(as.numeric(end\_lng), 2)

`  `)
### Calculo distancia total
clean\_Total\_data$distancia\_total <- distVincentySphere(

`  `p1 = cbind(clean\_Total\_data$start\_lng, clean\_Total\_data$start\_lat),

`  `p2 = cbind(clean\_Total\_data$end\_lng, clean\_Total\_data$end\_lat)

)
### Calculo tiempo de uso
clean\_Total\_data$started\_at <- ymd\_hms(clean\_Total\_data$started\_at)

\## Warning: 17 failed to parse.

clean\_Total\_data$ended\_at <- ymd\_hms(clean\_Total\_data$ended\_at)

\## Warning: 16 failed to parse.

clean\_Total\_data$tiempo\_de\_uso <- difftime(clean\_Total\_data$ended\_at, clean\_Total\_data$started\_at, units = "secs")

clean\_Total\_data$tiempo\_formateado <- seconds\_to\_period(clean\_Total\_data$tiempo\_de\_uso)

clean\_Total\_data$dia\_numero <- wday(clean\_Total\_data$started\_at)
### Validacion de que no existe otro tipo de elemento aparte de los necesarios en tipos de miembros
contador\_tipos <- clean\_Total\_data %>%

`  `group\_by(member\_casual) %>%

`  `summarize(contador = n())
### Validacion de que no existe otro tipo de elemento aparte de los necesarios en Tipos de bike
contador\_tipos2 <- clean\_Total\_data %>%

`  `group\_by(rideable\_type) %>%

`  `summarize(contador = n())
### Separacion de dia mes y año en diferentes columnas
clean\_Total\_data$dia <- day(clean\_Total\_data$started\_at)

clean\_Total\_data$mes <- month(clean\_Total\_data$started\_at)

clean\_Total\_data$anio <- year(clean\_Total\_data$started\_at)
## Analisis
### Dia con mas viajes realizados
filter\_Dia\_mas\_usado<- clean\_Total\_data %>%

`  `group\_by(dia\_numero,member\_casual) %>%

`  `summarise(count=n()) %>% 

`  `na.omit()

\## `summarise()` has grouped output by 'dia\_numero'. You can override using the

\## `.groups` argument.

View(filter\_Dia\_mas\_usado)
### cantidad de viajes en total
filter\_cantidad\_total<- clean\_Total\_data %>%

`  `group\_by(member\_casual) %>%

`  `summarise(count=n())
### Filtrar y agrupar los datos por tipo de bicicleta y tipo de usuario
viajes\_por\_bicicleta\_y\_usuario <- clean\_Total\_data %>%

`  `group\_by(rideable\_type, member\_casual) %>%

`  `summarize(cantidad\_viajes = n())

\## `summarise()` has grouped output by 'rideable\_type'. You can override using the

\## `.groups` argument.
### Filtrar los valores negativos
clean\_Total\_data <- clean\_Total\_data %>%

`  `mutate(tiempo\_de\_uso = as.numeric(sub(" secs", "", tiempo\_de\_uso))) %>%

`  `filter(tiempo\_de\_uso >= 300)
### Agrupar por tipo de usuario y calcular estadísticas Media,MIN,MAX, AVG
estadisticas\_viajes <- clean\_Total\_data %>%

`  `group\_by(member\_casual) %>%

`  `summarize(

`    `media = mean(tiempo\_de\_uso),

`    `maximo = max(tiempo\_de\_uso),

`    `minimo = min(tiempo\_de\_uso),

`    `promedio = median(tiempo\_de\_uso)

`  `)
### Agrupar por tipo de usuario y calcular estadísticas Media,MIN,MAX, AVG ahora por cada dia de la semana
estadisticas\_viajes\_dia <- clean\_Total\_data %>%

`  `group\_by(dia\_numero,member\_casual) %>%

`  `summarize(

`    `media = mean(tiempo\_de\_uso),

`    `maximo = max(tiempo\_de\_uso),

`    `minimo = min(tiempo\_de\_uso),

`    `promedio = median(tiempo\_de\_uso)

`  `)

\## `summarise()` has grouped output by 'dia\_numero'. You can override using the

\## `.groups` argument.
### Hacer una comparacion entre dias de semana y fin de semana
clean\_Total\_data$tipo\_semana <- ifelse(clean\_Total\_data$dia\_numero %in% c(6, 7), "fin\_de\_semana", "día\_laborable")

estadisticas\_dia\_tipo <- clean\_Total\_data %>%

`  `group\_by(tipo\_semana,member\_casual) %>%

`  `summarize(

`    `media = mean(tiempo\_de\_uso),

`    `maximo = max(tiempo\_de\_uso),

`    `minimo = min(tiempo\_de\_uso),

`    `promedio = median(tiempo\_de\_uso)

`  `)

\## `summarise()` has grouped output by 'tipo\_semana'. You can override using the

\## `.groups` argument.
### Tiempo de uso de cada mes diferenciado por tipo de miembro
estadisticas\_mes\_tipo <- clean\_Total\_data %>%

`  `group\_by(mes, member\_casual) %>%

`  `summarize(

`    `media = mean(tiempo\_de\_uso),

`    `maximo = max(tiempo\_de\_uso),

`    `minimo = min(tiempo\_de\_uso),

`    `promedio = median(tiempo\_de\_uso)

`  `)

\## `summarise()` has grouped output by 'mes'. You can override using the `.groups`

\## argument.
### Filtrar los viajes que marcan distancia recorrida en 0 y que tengan tiempo mayor a 0
viajes\_recorrido\_cero <- clean\_Total\_data %>%

`  `filter(distancia\_total == 0, tiempo\_de\_uso > 300) %>% 

`  `group\_by(member\_casual) %>% 

`  `summarize(

`    `media = mean(tiempo\_de\_uso),

`    `maximo = max(tiempo\_de\_uso),

`    `minimo = min(tiempo\_de\_uso),

`    `promedio = median(tiempo\_de\_uso)

`  `)
### Cantidad de viajes realizados dependiendo del usuario cuando llegan al mimso destino
viajes\_recorrido\_cero\_tipo <- clean\_Total\_data %>%

`  `filter(distancia\_total == 0, tiempo\_de\_uso > 300) %>% 

`  `group\_by(member\_casual) %>%  

`  `summarize(cantidad\_filas = n())  
### Viajes realizados por hora
viajes\_por\_hora <- clean\_Total\_data %>%

`  `mutate(hora = hour(started\_at)) %>%  # Extraer la hora del inicio del viaje

`  `group\_by(hora, member\_casual) %>%

`  `summarize(cantidad\_viajes = n())

\## `summarise()` has grouped output by 'hora'. You can override using the

\## `.groups` argument.
## Visualizaciones
## Crear un gráfico de barras apiladas para comparar el uso de bicicletas por tipo de usuario
ggplot(data = viajes\_por\_bicicleta\_y\_usuario, aes(x = rideable\_type, y = cantidad\_viajes, fill = member\_casual)) +

`  `geom\_bar(stat = "identity", position = "stack") +

`  `labs(title = "Uso de Bicicletas por Tipo de Usuario",

`       `x = "Tipo de Bicicleta",

`       `y = "Cantidad de Viajes",

`       `fill = "Tipo de Usuario") +

`  `theme\_minimal()

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.001.png)
# Comparacion de viajes recorridos cuando se llega al mismo destino de partida
ggplot(data = viajes\_recorrido\_cero\_tipo, aes(x = member\_casual, y = cantidad\_filas, fill = member\_casual)) +

`  `geom\_bar(stat = "identity") +

`  `labs(title = "Cantidad de Viajes con Recorrido en 0 por Tipo de Usuario",

`       `x = "Tipo de Usuario",

`       `y = "Cantidad de Viajes") +

`  `theme\_minimal()

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.002.png)
### Comparacion de cantidad de viajes
ggplot(data = filter\_cantidad\_total, aes(x = member\_casual, y = count, fill = member\_casual)) +

`  `geom\_bar(stat = "identity") +

`  `labs(title = "Cantidad de Viajes en total por Tipo de Usuario",

`       `x = "Tipo de Usuario",

`       `y = "Cantidad de Viajes") +

`  `theme\_minimal()+ 

`  `scale\_y\_continuous(labels = function(x) paste0(x/1e6, "M"))

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.003.png)
### Calcular la cantidad de viajes por mes y tipo de usuario
viajes\_por\_mes\_tipo <- clean\_Total\_data %>%

`  `mutate(mes = floor\_date(started\_at, unit = "month")) %>%

`  `group\_by(mes, member\_casual) %>%

`  `summarise(cantidad\_viajes = n())

\## `summarise()` has grouped output by 'mes'. You can override using the `.groups`

\## argument.
### Calcular la cantidad de viajes por mes y tipo de usuario
viajes\_por\_mes\_tipo <- clean\_Total\_data %>%

`  `mutate(mes = floor\_date(started\_at, unit = "month")) %>%

`  `group\_by(mes, member\_casual) %>%

`  `summarise(cantidad\_viajes = n())

\## `summarise()` has grouped output by 'mes'. You can override using the `.groups`

\## argument.

#Grafico de comparacion de viajes por dia de semana

ggplot(filter\_Dia\_mas\_usado, aes(x = dia\_numero, y = count, fill = member\_casual)) +

`  `geom\_bar(stat = "identity", position = "dodge") +

`  `labs(title = "Cantidad de Viajes por Día de la Semana y Tipo de Usuario",

`       `x = "Día de la Semana",

`       `y = "Cantidad de Viajes",

`       `fill = "Tipo de Usuario") +

`  `theme\_minimal() +

`  `scale\_x\_continuous(breaks = 1:7, labels = c( "Lun", "Mar", "Mié", "Jue", "Vie", "Sáb","Dom"))+

`  `scale\_y\_continuous(labels = function(x) paste0(x/1e6, "M"))

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.004.png)
### Crear un gráfico de líneas Cantidad de Viajes por Mes y Tipo de Usuario
ggplot(data = viajes\_por\_mes\_tipo, aes(x = mes, y = cantidad\_viajes, color = member\_casual)) +

`  `geom\_line() +

`  `labs(title = "Cantidad de Viajes por Mes y Tipo de Usuario",

`       `x = "Mes",

`       `y = "Cantidad de Viajes",

`       `color = "Tipo de Usuario") +

`  `theme\_minimal()+ 

`  `scale\_y\_continuous(labels = function(x) paste0(x/1e6, "M"))

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.005.png)
### Gráfico de Dispersión: Duración vs. Distancia
ggplot(clean\_Total\_data, aes(x = tiempo\_de\_uso, y = distancia\_total)) +

`  `geom\_point() +

`  `labs(title = "Gráfico de Dispersión: Duración vs. Distancia",

`       `x = "Duración del Viaje (minutos)",

`       `y = "Distancia Recorrida (km)") +

`  `theme\_minimal()

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.006.png)
### Gráfico de caja Boxplot: Duración del Viaje
ggplot(clean\_Total\_data, aes(x = 1, y = tiempo\_de\_uso)) +

`  `geom\_boxplot() +

`  `labs(title = "Boxplot: Duración del Viaje",

`       `x = "",

`       `y = "Duración del Viaje (minutos)") +

`  `theme\_minimal() +

`  `coord\_flip()

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.007.png)
### Crear un gráfico de barras para viajes por hora
ggplot(data = viajes\_por\_hora, aes(x = hora, y = cantidad\_viajes, fill = member\_casual)) +

`  `geom\_bar(stat = "identity", position = "dodge") +

`  `labs(title = "Cantidad de Viajes por Hora del Día",

`       `x = "Hora del Día",

`       `y = "Cantidad de Viajes",

`       `fill = "Tipo de Usuario") +

`  `theme\_minimal()

![](Aspose.Words.230be4ca-33f0-4306-aeee-5a30c98ccf8f.008.png)

view(clean\_Total\_data)
# Exportacion de datos utilizados
campos\_utilizados <- clean\_Total\_data %>%

`  `select(

`    `ride\_id, rideable\_type, started\_at, ended\_at, member\_casual,

`    `distancia\_total, tiempo\_de\_uso, dia\_numero, dia, mes, anio

`  `)

ruta\_salida <- "C:/Users/felip/OneDrive/Documentos/R/Cyclistic/Datos\_Analizados.csv" 

write\_csv(campos\_utilizados, ruta\_salida)
