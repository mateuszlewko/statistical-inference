# Lista 2

Mateusz Lewko

## Zadanie 1

```R
dane1 <- read.csv("w-02-01.csv")
nrow(dane1)
summary(dane1)
dane1 <- as.matrix(dane1)
mean(dane1)
var(dane1)
```

a) Wariancja: 80.61845, średnia: 15.98333, n: 300

```R
se <- function(x) sqrt(var(x) / length(x))
se(dane1)

(half <- qnorm(0.975) * sd(dane1) / sqrt(nrow(dane1)))
(left <- mean(dane1) - half)
(right <- mean(dane1) + half)
```

b) Przedział ufności: [14.96731, 16.99936]

## Zadanie 2

```R
mu0 <- 18.0
z <- (mean(dane1) - mu0) / ( sd(dane1)/sqrt(length(dane1)) )
z
qnorm(0.975)
2 * pnorm(z)
```

wartość_p: 0.000100141, odrzucamy H0

## Zadanie 3

```R
mu0 <- 17.0
z <- (mean(dane1) - mu0) / ( sd(dane1)/sqrt(length(dane1)) )
z
qnorm(0.975)
2 * pnorm(z)
```

wartość_p: 0.04985564, na granicy - można odrzucić H0

## Zadanie 4

```R
dane2 <- read.csv("w-02-04.csv")
(n <- nrow(dane2)) # 15 -> małe dane
summary(dane2)
dane2 <- as.matrix(dane2)
mean(dane2)
var(dane2)
```

a) i c) H0: mu = 2750

```R
mu0 <- 2750
t <- (mean(dane2) - mu0) / ( sd(dane2)/sqrt(length(dane2)) )

2 * (1 - pt(t, df=n-1))
```
wartość_p: 0.2264394

b) Przedział ufności

```R
(half <- qt(0.975, df=n-1) * sd(dane2)/sqrt(n))
(left <- mean(dane2) - half)
(right <- mean(dane2) + half)
```

Przedział [2689.567, 2984.3]

## Zadanie 5

b) Przedział ufności

```R
p <- 52/215
q <- 1.0 - p
(half <- qnorm(0.975) * sqrt(p * q / 215))
(right <- p + half)
(left <- p - half)
```

przedział: [0.1846223, 0.2990987]

a) i c) H0: p = 0.22

```R
z <- (p - 0.22) / sqrt((0.22 * (1 - 0.22)) / 215)
z

qnorm(0.975)
2 - 2 * pnorm(z)
```

wartość_p: 0.4390583, nie ma podstaw do odrzucenia H0

## Zadanie 8

a) N(0, 1), N(0, 2)

```R
require(ggplot2)
x <- seq(-20, 20, 0.01)
y1 <- dnorm(x)
y2 <- dnorm(x, sd=2)

df <- data.frame(x, y1, y2)
g <- ggplot(df, aes(x))
g <- g + geom_line(aes(y=y1), colour="red")
g <- g + geom_line(aes(y=y2), colour="green")
g
```

b) N(0, 1), N(1, 1)

```R
x <- seq(-4, 4, 0.01)
y1 <- dnorm(x)
y2 <- dnorm(x, mean=1)

df <- data.frame(x, y1, y2)
g <- ggplot(df, aes(x))
g <- g + geom_line(aes(y=y1), colour="red")
g <- g + geom_line(aes(y=y2), colour="green")
g
```

c) t10, t5, N(0, 1)

```R
x <- seq(-4, 4, 0.01)
y1 <- dnorm(x)
y2 <- dt(x, 5)
y3 <- dt(x, 10)

df <- data.frame(x, y1, y2, y3)
g <- ggplot(df, aes(x))
g <- g + geom_line(aes(y=y1), colour="red")
g <- g + geom_line(aes(y=y2), colour="green")
g <- g + geom_line(aes(y=y3), colour="blue")
g
```

d) t10, t5, N(0, 1)

```R
x <- seq(0, 20, 0.01)
y1 <- dchisq(x, df=4)
y2 <- dchisq(x, df=6)
y3 <- dchisq(x, df=8)

df <- data.frame(x, y1, y2, y3)
g <- ggplot(df, aes(x))
g <- g + geom_line(aes(y=y1), colour="red")
g <- g + geom_line(aes(y=y2), colour="green")
g <- g + geom_line(aes(y=y3), colour="blue")
g
```