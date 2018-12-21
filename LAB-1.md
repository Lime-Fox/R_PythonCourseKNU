# **LAB-1**

## **TASK-1** - Задание переменных
**Задать данные базових (atomic) типов - `integer`, `numeric`, `complex`, `logical`, `character`:** 

```
dt_integer<-1L
dt_numeric<-1.5
dt_complex<-1 + 1i
dt_logical<-TRUE
dt_character<-"abc"

class(dt_integer)
class(dt_numeric)
class(dt_complex)
class(dt_logical)
class(dt_character)
```
```
[1] "integer"
[1] "numeric"
[1] "complex"
[1] "logical"
[1] "character"
```

## **TASK-2** - Задание векторов
**Задать следующие векторы:**
* Вектор содержат последовательность от 5 до 75
* Вектор содержит числа 3.14, 2.71, 0, 13
* Вектор содержит 100 значень TRUE
 
```
v1<-c(5:75)
v1
v2<-c(3.14, 2.71, 0.0, 13)
v2
v3<-c(rep(TRUE, 100))
v3
```
```
[1]  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40
[37] 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75

[1]  3.14  2.71  0.00 13.00

[1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
[22] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
[43] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
[64] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
[85] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
```

## **TASK-3** - Задание матриц
**Задать следующую матрицу**

```0.5 1.3 3.5```

```3.9 131.0 2.8``` 

```0.0 2.2 4.6``` 

```2.0 7.0 5.1``` 

**с помощью:**

```СПОСОБ 1```
* Функция **matrix** - формирует матрицу (по столбцам)
```
v4 <- c(0.5, 1.3, 3.5, 3.9, 131.0, 2.8, 0.0, 2.2, 4.6, 2.0, 7.0, 5.1)
m<-matrix(v4,nrow=4,ncol=3,byrow=TRUE)
m
```
```
     [,1]  [,2] [,3]
[1,]  0.5   1.3  3.5
[2,]  3.9 131.0  2.8
[3,]  0.0   2.2  4.6
[4,]  2.0   7.0  5.1
```

```СПОСОБ 2```
* Функция `rbind` - объединяет аргументы (по строкам)
```
v5 <- c(0.5, 1.3, 3.5, 3.9, 131.0, 2.8, 0.0, 2.2, 4.6, 2.0, 7.0, 5.1)
rb<- rbind(v5[1:3], v5[4:6], v5[7:9], v5[10:12])
rb
```
```
      [,1]  [,2] [,3]
[1,]  0.5   1.3  3.5
[2,]  3.9 131.0  2.8
[3,]  0.0   2.2  4.6
[4,]  2.0   7.0  5.1
```

* Функция `сbind` - объединяет аргументы (по столбцам)
```
v6 <- c(0.5, 3.9, 0.0, 2.0, 1.3, 131.0, 2.2, 7.0, 3.5, 2.8, 4.6, 5.1)
cb<- cbind(v6[1:4], v6[5:8], v6[9:12])
cb
```
```
      [,1]  [,2] [,3]
[1,]  0.5   1.3  3.5
[2,]  3.9 131.0  2.8
[3,]  0.0   2.2  4.6
[4,]  2.0   7.0  5.1
```

```СПОСОБ 3```
* Функция `dim` - формирует матрицу заданной размерности (по столбцам)
```
v7 <- c(0.5, 3.9, 0, 2, 1.3, 131, 2.2, 7, 3.5, 2.8, 4.6, 5.1)
dim(v7)<-c(4,3)
v7
```
```
      [,1]  [,2] [,3]
[1,]  0.5   1.3  3.5
[2,]  3.9 131.0  2.8
[3,]  0.0   2.2  4.6
[4,]  2.0   7.0  5.1
```
>Также с помощью функции dim можно проверить размерность матрицы:
```
dim(v7)
```
```
[1] 4 3
```
