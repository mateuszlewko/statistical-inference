# Lista 8

Mateusz Lewko

## Zadanie 1

```R
sum = 20 + 25 + 60 + 45
sum
# [1] 150

skladnik <- function (obs, e) { (obs - sum * e)^2 / (sum * e) }
z = skladnik(20, 0.1) + skladnik(25, 0.2) + skladnik(50, 0.5) + skladnik(45, 0.2

# 3 stopnie swobody 
pchisq(z, df = 3)
# 0.9996246
```

Odrzucamy H0.

## Zadanie 2

H0: p = 0.5

```R
pbinom(12, 20, .5)
# [1] 0.868412
# > 1 - 0.868412
# [1] 0.131588
```

wartość_p =  0.131588
Nie odrzucamy H0, napoje są podobne

## Zadanie 3

```R
sum = 90
z = skladnik(35, 1/3) + skladnik(40, 1/3) + skladnik(15, 1/3)
z
# [1] 11.66667
pchisq(z, df = 2)
# [1] 0.9970717
```

Odrzucamy H0, kostka nie jest prawidłowa

## Zadanie 4

H0: p = 0.5

```R
pbinom(24, 40, .5)
# [1] 0.92307
> 1 - 0.92307
# [1] 0.07693
```

wartość_p = 0.07693
(Raczej) nie odrzucamy H0, napoje są dość podobne

## Zadanie 5

| Stan | Kat | Prot | Inni |
|------|-----|------|------|
| M    | 135 | 130  | 60   |
| R    | 40  | 50   | 25   |
| S    | 25  | 20   | 15   |

suma = 135 + 130 + 60 + 40 + 50 + 25 + 25 + 20 + 15 = 500

a = 135/500 + 40/500 + 25/500

b = 130/500 + 50/500 + 20/500

c = 60/500  + 25/500 + 15/500

|Pi.  | (a) | (b)  | (c) | P.j  |
|-----|-----|------|-----|------|
|     | a*x |  ... |     | x = 135/500 + 130/500 + 60/500
|     |     |      |     | y = 40/500  + 50/500  + 25/500
|     |     |      |     | z = 25/500  + 20/500  + 15/500

```R

> a = 135/500 + 40/500 + 25/500
> b = 130/500 + 50/500 + 20/500
> c = 60/500  + 25/500 + 15/500
> x = 135/500 + 130/500 + 60/500
> y = 40/500  + 50/500  + 25/500
> z = 25/500  + 20/500  + 15/500
> Y = c(x,y,z)
> X = c(a, b, c)
> X %*% t(Y)
#      [,1]  [,2]  [,3]
# [1,] 0.26 0.092 0.048
# [2,] 0.26 0.092 0.048
# [3,] 0.13 0.046 0.024
> (X %*% t(Y))*500
#      [,1] [,2] [,3]
# [1,]  130   46   24
# [2,]  130   46   24
# [3,]   65   23   12
```

Stan cywilny jest zależny od wyznania

## Zadanie 6

```R
> data <- as.matrix(read.csv("ww-0806.csv", header=FALSE))
> median(data)
# [1] 13
```

25 obserwacji

H0: mediana = 10

13 obserwacji jest większe od mediany

Jeśli mediana wynosi 10, to zmienna

     X = { 0 gdy losowo wybrana liczba ze zbioru jest >= 10
           1 gdy jest < 10
         }
    jest z rozkładu B(25, 1/2)

```R
pbinom(13, 25, .5)
# [1] 0.654981
1 - 0.654981 = 0.34
```

Mediana może być równa 10.

## Zadanie 7

a) TAK

```R
> .45 * 500
[1] 225
> .4 * 500
[1] 200
> .1 * 500
[1] 50
> .05 * 500
[1] 25
```

b) TAK

```R
sum = 500
z = skladnik(250, 0.45) + skladnik(175, 0.4) + skladnik(50, .1) + skladnik(25, 0.05)
z
# [1] 5.902778
```

c) NIE (są 3 stopnie swobody)

d) TAK

```R
> 1 - pchisq(z, df = 3)
# [1] 0.1164373 ~ 0.12
```

## Zadanie 8

3 obserwacje 
```
Możliwe przynależności do grupy
+ + + | 1+2+3=6
+ + - | 1+2-3=0
+ - + | 1-2+3=2
+ - - | 1-2-3=-4
- + + | -1+2+3=4
- + - | -1+2-3=-2
- - + | -1-2+3=0
- - - | -1-2-3=-6
```
rozkład: 
    1/8 dla {-6, -4, -2, 2, 4, 6}
    1/4 dla 0 

## Zadanie 9

a) NIE, mam 12 komórek
b) TAK

```R
> 1 - pchisq(19.46, df = 6)
# [1] 0.003453345
```

c) NIE
d) Raczej nie, bo mamy podstawę do odrzucenia H0

## Zadanie 10

```R
(data <- as.matrix(read.csv("ww-0810.csv", sep=';')))

> summary(data[,1])
#    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#   25.00   69.25   75.50   76.18   87.75   98.00 
> summary(data[,2])
#    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#   30.00   65.00   70.50   69.66   77.75   91.00 

> wilcox.test(data[,1], data[,2])

	Wilcoxon rank sum test with continuity correction

data:  data[, 1] and data[, 2]
W = 1643, p-value = 0.006768
alternative hypothesis: true location shift is not equal to 0
```

wartość_p = 0.006768, jest różnica w medianach

## Zadanie 11

```R
(data <- as.matrix(read.csv("ww-0811.csv", sep=';')))
#       Papierosy Cisnienie
#  [1,]        30        95
#  [2,]        20       100
#  [3,]        25        90
#  [4,]        40       110
#  [5,]        20        95
#  [6,]        25        93
#  [7,]        35        85
#  [8,]        20        90
#  [9,]        60       115
# [10,]        35        95

> cor(data, method="kendal")
#           Papierosy Cisnienie
# Papierosy 1.0000000 0.2963189
# Cisnienie 0.2963189 1.0000000
> cor(data, method="spearman")
#           Papierosy Cisnienie
# Papierosy  1.000000  0.366773
# Cisnienie  0.366773  1.000000

install.packages("GoodmanKruskal")
require("GoodmanKruskal")

GKtau(data[,1], data[,2])
#       xName     yName Nx Ny tauxy tauyx
# 1 data[, 1] data[, 2]  6  7 0.512 0.625

install.packages("DescTools")
> require("DescTools")
> SomersDelta(data[,1], data[,2])
# [1] 0.2926829
```

## Zadanie 12

Cena	Pokoje	Inne
154	    3    	3
176	    4    	3
164	    4    	3
242	    5    	3
160	    3    	4
223	    4    	4
230	    5    	4
227	    4    	5
259	    5    	5
231	    5    	5
(zapisane do pliku ww-0812.csv)

```R
# a) 

> (data <- read.csv("ww-0812.csv", sep=','))

> lm(data$Cena ~ data$Pokoje + data$Inne)

# Call:
# lm(formula = data$Cena ~ data$Pokoje + data$Inne)

# Coefficients:
# (Intercept)  data$Pokoje    data$Inne  
#      -5.047       35.722       15.799  

# b) 
> (fit <- aov(Cena ~ Pokoje + Inne, data=data))
# Call:
#    aov(formula = Cena ~ Pokoje + Inne, data = data)

# Terms:
#                   Pokoje     Inne Residuals
# Sum of Squares  9844.829 1506.530  2165.041
# Deg. of Freedom        1        1         7

# Residual standard error: 17.58669
# Estimated effects may be unbalanced
> summary(fit)
#             Df Sum Sq Mean Sq F value   Pr(>F)    
# Pokoje       1   9845    9845  31.830 0.000781 ***
# Inne         1   1507    1507   4.871 0.063075 .  
# Residuals    7   2165     309                     
# ---
# Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```