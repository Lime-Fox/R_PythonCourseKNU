# **LAB-5**
**АНАЛИЗ ЗАГРЯЗНЕНИЯ ОКРУЖАЮЩЕЙ СРЕДЫ**

## **TASK-1**

* Написать функцию `pmean`, которая считает среднее значение (mean)
загрязнения сульфатами или нитратами среди данного перечня мониторов.
```
Данная функция принимает 3 аргумента: 
«directory» - папка в которой находятся данные 
«pollutant» - вид загрязнения
«id» - список мониторов 
По умолчанию аргумент id имеет значение 1:332.
(функція должна игнорировать NA значения) 
```
```
ПРИМЕРЫ РАБОТЫ ФУНКЦИИ:

pmean("specdata", "sulfate", 1:10)
## [1] 4.064128

pmean("specdata", "sulfate", 55)
## [1] 3.587319

pmean("specdata", "nitrate")
## [1] 1.702932
```
```
NEW.FILE <- function(name) {
  l <- 3L
  name <- paste('000', name, sep = '')
  
  return(paste(substr(
    name,
    nchar(name) - l+1,
    nchar(name)
  ), '.csv', sep = ''))
}

pmean <- function(directory, pollutant, id = c(1:332)) {
    way <-
    paste('C:/Users/USER/data/', directory, '/', sep = "")
    cifra <- c()
  
  for (i in id) {
    rf<-
    read.csv(file = paste(way, NEW.FILE(i), sep = ""))
    cn <- colnames(rf)
    
    if (pollutant %in% cn) {
      cifra <- c(cifra, rf[, pollutant, drop = TRUE])
    }
  }
  return(mean(cifra, na.rm = TRUE))
}


#ПРОВЕРКА:

t1 <- pmean("specdata", "sulfate", 1:10)
t1
t2 <- pmean("specdata", "sulfate", 55)
t2
t3 <- pmean("specdata", "nitrate")
t3
```
```
[1] 4.064128
[1] 3.587319
[1] 1.702932
```

## **TASK-2**

* Написать функцию `complete`, которая выводит количество полных наблюдений
(the number of completely observed cases) для каждого файла. 
```
Данная функция принимает 2 аргумента: 
«directory» 
«id» 
и возвращает data frame: 1ый столбец – имя файла, 2ой – кол-во полных наблюдений
```
```
ПРИМЕРЫ РАБОТЫ ФУНКЦИИ:

complete("specdata", 1)
##   id nobs
## 1 1 117

complete("specdata", c(2, 4, 8, 10, 12))
##   id nobs
## 1 2 1041
## 2 4 474
## 3 8 192
## 4 10 148
## 5 12 96

complete("specdata", 50:60)
##   id nobs
## 1 50 459
## 2 51 193
## 3 52 812
## 4 53 342
## 5 54 219
## 6 55 372
## 7 56 642
## 8 57 452
## 9 58 391
## 10 59 445
## 11 60 448
```
```
complete <- function(directory, id) {
    way <-
    paste('C:/Users/USER/data/', directory, '/', sep = "")
    d.base <- data.frame(filename = character(), count = integer())
  
  for (i in id) {
    sup.file<- NEW.FILE(i)
    
    rf <-
      read.csv(file = paste(way, sup.file, sep = ""))
    
      ad.plus <- sum(!is.na(rf['nitrate'] & rf['sulfate']))
    
      form.vec <- list(id = sup.file, nobs = ad.plus)
      d.base = rbind(d.base, form.vec, stringsAsFactors = FALSE)
  }
  
  return(d.base)
}

#ПРОВЕРКА:

a <- complete("specdata", 1)
a
b <- complete("specdata", c(2, 4, 8, 10, 12))
b
c <- complete("specdata", 50:60)
c
```
```
        id nobs
1 001.csv  117

        id nobs
1 002.csv 1041
2 004.csv  474
3 008.csv  192
4 010.csv  148
5 012.csv   96

        id nobs
1  050.csv  459
2  051.csv  193
3  052.csv  812
4  053.csv  342
5  054.csv  219
6  055.csv  372
7  056.csv  642
8  057.csv  452
9  058.csv  391
10 059.csv  445
11 060.csv  448
```


## **TASK-3**

* Написать функцию `corr`
```
Данная функция принимает 2 аргумента: 
directory (папка, где находяться файлы наблюдений)
threshold (пороговое значение, по умолчанию=0) 
и считает корреляцию между сульфатами и нитратами для мониторов, 
кол-во полных наблюдений для которых больше порогового значення. 

Функция должна вернуть вектор значений корреляций.
Если ни один монитор не превышает порогового значения,
функция должна вернуть numeric вектор ддлинною = 0. 

Для расчета корреляции между сульфатами та нитратами - 
функция «cor» с параметрами по умолчанию.
```
```
ПРИМЕРЫ РАБОТЫ ФУНКЦИИ:

cr <- corr("specdata", 150)
head(cr); summary(cr)
## [1] -0.01895754 -0.14051254 -0.04389737 -0.06815956 -0.12350667 -
0.07588814
## Min. 1st Qu. Median Mean 3rd Qu. Max.
## -0.21060 -0.04999 0.09463 0.12530 0.26840 0.76310

cr <- corr("specdata", 400)
head(cr); summary(cr)
## [1] -0.01895754 -0.04389737 -0.06815956 -0.07588814 0.76312884 -
0.15782860
## Min. 1st Qu. Median Mean 3rd Qu. Max.
## -0.17620 -0.03109 0.10020 0.13970 0.26850 0.76310

cr <- corr("specdata", 5000)
head(cr); summary(cr) ; length(cr)
## NULL
## Length Class Mode
## 0 NULL NULL
## [1] 0
```
