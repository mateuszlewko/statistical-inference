# Lista 1.
Mateusz Lewko

## Zadanie 1

```R
dane <- read.csv("ww0101.csv")
nrow(dane) # 300
summary(dane)
dane <- as.matrix(dane)
mean(dane)
var(dane)
sd(dane)

se <- function(x) sqrt(var(x) / length(x))
se(dane)

(half <- qnorm(0.975) * sd(dane) / sqrt(nrow(dane)))
(left <- mean(dane) - half) # 15.05
(right <- mean(dane) + half) # 17.12

```
mu0 = 18.0 poza przedziałem ufności [15.05, 17.12], odrzucamy H0.

## Zadanie 2

```R
mu0 <- 17.5
z <- (mean(dane) - mu0) / ( sd(dane)/sqrt(length(dane)) )
z
qnorm(0.975)
2 * pnorm(z)
```

wartość_p: 0.007318915, odrzucamy H0.

## Zadanie 3

```R
dane2 <- read.csv("ww0102.csv")
dane2 <- as.matrix(dane2)
(n <- nrow(dane2)) # 15

# Małe dane
# a) Przedział ufności

(half <- qt(0.975, df=n-1) * sd(dane2)/sqrt(nrow(dane2)))
(left <- mean(dane2) - half)
(right <- mean(dane2) + half)

# przedział: [2689.567, 2984.3]

# b) Hipoteza H0: mu0 = 2830
mu0 <- 2830
t <- (mean(dane2) - mu0) / ( sd(dane2)/sqrt(length(dane2)) )

2 * (1 - pt(t, df=n-1)) # 0.9210539
```
wartość_p: 0.9210539, nie ma podstaw do odrzucenia H0.

## Zadanie 4

```R
require(ggplot2)
x <- seq(0, 2, 0.01)
y1 <- dnorm(x)
y2 <- dt(x, 3)
y3 <- dt(x, 25)

df <- data.frame(x, y1, y2, y3)
g <- ggplot(df, aes(x))
g <- g + geom_line(aes(y=y1), colour="red")
g <- g + geom_line(aes(y=y2), colour="green")
g <- g + geom_line(aes(y=y3), colour="blue")
g
```

## Zadanie 5

```R
# a) Przedział ufności

p <- 11.0/35.0
q <- 1.0 - p
(half <- qnorm(0.975) * sqrt(p * q / 350.0))
(right <- p + half) # 0.3629206
(left <- p - half)  # 0.2656508

# przedział: [0.2656508, 0.3629206]

# b) i c) 
# a = 0.05, test H0: p0 = 1/3, wyznaczyć wartość_p

z <- (p - 1/3) / sqrt((3/9) / 350)
z

qnorm(0.975) # 1.959964
2 * pnorm(z) # 0.537094
```

wartość_p = 0.537094, nie ma podstaw do odrzucenia H0.