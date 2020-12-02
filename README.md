# uts-dmkm
Tugas responsi

library(party)
library(psych)
library(caret)

## Membaca Data 
data <- read.csv("D:/3SI2/DMKM/UTS/data.csv", header=FALSE)
head(data)

## Kategorisasi Data
data$V1 <- as.factor(data$V1)
data$V2 <- as.factor(data$V2)
data$V3 <- as.factor(data$V3)
data$V4 <- as.factor(data$V4)
data$V6 <- as.factor(data$V6)
str(data)

## Training dan Testing
set.seed(1234)
sampel <- sample(2, nrow(data),replace = T, prob = c(0.8, 0.2))
trainingdat <- data[sampel==1, ]
testingdat <- data[sampel==2, ]
print(paste("Jumlah train data :", nrow(trainingdat)))
print(paste("Jumlah test data :", nrow(testingdat)))

## Running dan Visualisasi
pohonnya <- ctree(V6~., data=trainingdat)
plot(pohonnya)

## Evaluasi Model
prediksi <- predict(pohonnya, testingdat)
confusionMatrix(table(prediksi,testingdat$V6))
