# Lista 4

Mateusz Lewko

## Zadanie 1

H0: średnia liczba ogłoszeń w trzech gazetach jest taka sama

```R
data <- read.csv("ww0401.csv", header=FALSE)
data$V1
# [1] 246 231 236 217 246 243 246 243 235 235 265 260 265 253 291

data$V2
# [1] A A A A A B B B B B C C C C C
# Levels: A B C

data <- data.frame(data)
summary(aov(V1 ~ V2, data))

#             Df Sum Sq Mean Sq F value Pr(>F)   
# V2           2   2871  1435.5   11.37 0.0017 **
# Residuals   12   1515   126.2                  
# ---
# Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```

Na poziomie wiarygodności 0.01 można odrzucić H0. Średnia liczba ogłoszeń 
jest różna.

## Zadanie 2

H0: liczba zgłoszeń jest średnio taka sama we wszystkich oddziałach

```R
(data <- data.frame(read.csv("ww0402.csv")))

# dopisanie etykiety oddziału
A <- rbind(data$A, rep('A', 18))
B <- rbind(data$B, rep('B', 18))
C <- rbind(data$C, rep('C', 18))
D <- rbind(data$D, rep('D', 18))

# złączenie 4 macierzy k x 2 w jedną (suma k) x 2
(data <- rbind(t(A), t(B), t(C), t(D)))
# usunięcie wierszy z NA, stworzenie data frame
(data <- data.frame(na.omit(data)))
# konwertowanie pierwszej kolumny na liczby
data$X1 <- as.numeric(as.character(data$X1))

summary(aov(X1 ~ X2, data))
#             Df Sum Sq Mean Sq F value   Pr(>F)    
# X2           3  390.1   130.0   17.57 3.12e-08 ***
# Residuals   58  429.3     7.4                     
# ---
# Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```

Średnia liczba zgłoszeń jest różna

## Zadanie 3

H0: punkty położone są w obrębie tej samej struk-tury geologicznej

```R
(data <- data.frame(read.csv("ww0403.csv")))

# dopisanie etykiety oddziału
A <- rbind(data$A, rep('A', 18))
B <- rbind(data$B, rep('B', 18))
C <- rbind(data$C, rep('C', 18))
D <- rbind(data$D, rep('D', 18))

# złączenie 4 macierzy k x 2 w jedną (suma k) x 2
(data <- rbind(t(A), t(B), t(C), t(D)))
# usunięcie wierszy z NA, stworzenie data frame
(data <- data.frame(na.omit(data)))
# konwertowanie pierwszej kolumny na liczby
data$X1 <- as.numeric(as.character(data$X1))

summary(aov(X1 ~ X2, data))
#             Df Sum Sq Mean Sq F value Pr(>F)
# X2           3    161   53.59   0.212  0.888
# Residuals   58  14655  252.67 
```

Brak podstaw do odrzucenia H0

## Zadanie 4

a) H0: średnia wytrzymałość opony jest niezależna od producenta 
       (średnia wytrzymałość jest taka sama)

b) H0: średnia wytrzymałość opony jest niezależna od producenta