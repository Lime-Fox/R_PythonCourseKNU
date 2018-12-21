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
* Вектор содержит последовательность от 5 до 75
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

```0.5   1.3   3.5```

```3.9   131.0 2.8``` 

```0.0   2.2   4.6``` 

```2.0   7.0   5.1``` 

**с помощью:**

```СПОСОБ 1```
* Функция `matrix` - формирует матрицу (по столбцам)
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

## **TASK-4** - Задание списков:

```ПУНКТ 1```

**Создадим список на основе базовых типов данных, (TASK-1):**
```
list1 <- list(dt_integer, dt_numeric, dt_complex, dt_logical, dt_character)
list1
```
```
[[1]]
[1] 1

[[2]]
[1] 1.5

[[3]]
[1] "abc"

[[4]]
[1] 1+1i

[[5]]
[1] TRUE
```

```ПУНКТ 2```

**Создадим список на основе нижеприведенных данных:**
```
list2 <- list(1:5,c(1,2,3,4,5),c(1+1i,1+2i,1+3i,1+4i,1+5i),c(TRUE,FALSE),c('HELLO!'))
list2
```
```
[[1]]
[1] 1 2 3 4 5

[[2]]
[1] 1 2 3 4 5

[[3]]
[1] 1+1i 1+2i 1+3i 1+4i 1+5i

[[4]]
[1]  TRUE FALSE

[[5]]
[1] "HELLO!"
```

## **TASK-5** - Задание фактора:
**Создать фактор с тремя уровнями «baby», «child», «adult»**

* Функция `factor` - формирует ранговый вектор, который содержит коды определеннных признаков
* Функция `levels` - формирует вектор признаков

* Зададим обычный вектор (значения будут упорядочены по алфавиту):

```
vsign<-c("baby","child","child","adult","baby","adult","baby","adult","child","adult","adult") 
f1<-factor(vsign)
f1
```
```
[1] baby child child adult baby adult baby adult child adult adult
Levels: adult baby child
```

* Для того чтобы получить значения признаков в нужном порядке:
```
vsign<-c("baby","child","child","adult","baby","adult","baby","adult","child","adult","adult") 
f2<-factor(vsign,levels=c("baby","child","adult"))
f2
```
```
[1] baby child child adult baby adult baby adult child adult adult
Levels: baby child adult
```

## **TASK-6** - Задание индексов и поиск кол-ва значений вектора
**Найти:**
* Индекс первого значения NA в векторе 1, 2, 3, 4, NA, 6, 7, NA, 9, NA, 11
* Количество значений NA
> Объяснение:

* `NA` - not available(нет в наличии) - пропущенные данные
* Функция `is.na(x)` - проверяет вектор на кол-во пропущенных значений
* Функция `match(x,y)` - сопоставляет значение объекта x со значением объекта y и возвращает поряд. номер 1го из совпадающих значений
* Функция `sum(x)` - сума значений вектора x

```
v8<-c(1, 2, 3, 4, NA, 6, 7, NA, 9, NA, 11)
i1<-match(NA,v8)
i1
```
```
[1] 5
```
```
qelement_NA1<-sum(is.na(v8))
qelement_NA1
```
```
[1] 3
```
## **TASK-7-8** - Задание data frame + изменение названий строк/столбцов
**Создать произвольный data frame и вывести в консоль**

>Объяснение:
* Функция `data.frame()` - задает массив данных различных типов
* Функция `names(data.frame())[№ Столбца]` - переименование названия столбца
* Функция `rownames()` - переименование названий строк фрейма
* Функция `colnames()` - переименование названий столбцов фрейма

```СПОСОБ 1 - Заданы только названия столбцов```

```
Name<-c("Anna","Mary","Jane")
Subject<-c("A","B","C")
Mark<-c(95,82,74)
SUCCESS<-data.frame(Name,Subject,Mark)
SUCCESS
```
```
Name    Subject Mark
1 Anna       A   95
2 Mary       B   82
3 Jane       C   74
```

```СПОСОБ 2 - Заданы названия строк и столбцов```

```
SUCCESS <- data.frame(c("Anna","Mary","Jane"), c("A","B","C"), c(95, 82, 74))
rownames(SUCCESS) <- c("№1","№2","№3")
colnames(SUCCESS)<-c("NAME","SUBJECT","MARK")
SUCCESS
```
```
   NAME  SUBJECT MARK
№1 Anna       A   95
№2 Mary       B   82
№3 Jane       C   74
```

>Поменяем названия строки№1 и столбца№1

```
rownames(SUCCESS)[1]<-"WINNER"
colnames(SUCCESS)[1]<-"FIRST NAME"
SUCCESS
```
```
        FIRST NAME SUBJECT MARK
WINNER       Anna       A   95
№2           Mary       B   82
№3           Jane       C   74
```
