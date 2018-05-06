# Lista 6 (regresja liniowa)

Mateusz Lewko

## Zadanie 1

Metoda 1

```R
SXX <- function(X) { sum((X - mean(X))^2) }
SXY <- function(X, Y) { sum((X - mean(X)) * (Y - mean(Y))) }

B1 <- function(X, Y) { SXY(X, Y) / SXX(X) }
B0 <- function(X, Y, b1) { mean(Y) - b1 * mean(X) }

# > B1(data$Czas, data$Wynik)
# [1] 1.636364
# > (b1 <- B1(data$Czas, data$Wynik))
# [1] 1.636364
# > (b0 <- B0(data$Czas, data$Wynik, b1))
# [1] 61.22727
```

Metoda 2

```R
data <- read.csv("ww0701.csv")
lm(data$Wynik ~ data$Czas)

# Coefficients:
# (Intercept)    data$Czas  
#      61.227        1.636 
```

B0 = 61.227
B1 = 1.636

## Zadanie 2

```R
data <- read.csv("ww0702.csv")
lm(data$Sprzedaż ~ data$Rok)

# Coefficients:
# (Intercept)     data$Rok  
#    22123.29       -10.96

2018 * -10.96 + 22123.29
# 6.01
```

Przewidywana sprzedaż to 6.01

## Zadanie 3

```R
Y_hat <- function(X, Y) {
    b1 <- B1(X, Y)
    b0 <- B0(X, Y, b1)
    X * b1 + b0
}

SE <- function(X, Y) {
    yh <- Y_hat(X, Y)
    n <- length(Y)
    sum((Y - yh)^2)/((n-2) * SXX(X))
}

data <- read.csv("ww0703.csv")
```

Hipoteza zerowa: B1 = 0 (ciśnienie nie zależy od wagi)

```R
(t <- B1(data$Ciśnienie, data$Waga) / SE(data$Ciśnienie, data$Waga))
# 25.24244

(df <- length(data$Waga) - 2)
# 8

pt(t, df=8)
# 1
```

Ciśnienie zależy od wagi.

## Zadanie 4

```R
data <- read.csv("ww0703.csv")

(r <- SXY(data$Ciśnienie, data$Waga) / sqrt(SXX(data$Ciśnienie) * SXX(data$Waga)))
# 0.8106536

cor(data)
#           Ciśnienie      Waga
# Ciśnienie 1.0000000 0.8106536
# Waga      0.8106536 1.0000000

cor(data, method="spearman")
#           Ciśnienie      Waga
# Ciśnienie 1.0000000 0.8409825
# Waga      0.8409825 1.0000000
```

## Zadanie 5

```R
data <- read.csv("ww0705.csv")

(r <- SXY(data$TV, data$Test) / sqrt(SXX(data$TV) * SXX(data$Test)))
# -0.8751346

(ssr <- sum((Y_hat(data$TV, data$Test) - mean(data$Test))^2))
# 2.968475
(sse <- sum((Y_hat(data$TV, data$Test) - data$Test)^2))
# 0.9075247

ssr / (sse + ssr)
# [1] 0.7658605
```

r = -0.8751346
r^2 = 0.9075247
