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

