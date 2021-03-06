# ⭕ ADP 모의고사 3회

## 1️⃣ 통계분석 (사용 데이터 Carseats)

### 1) urban변수에 따른 Sales의 차이가 있는지를 통계적으로 검증하기 위한 통계분석을 수행하고, 결과를 해석하시오.(데이터는 정규성을 만족한다고 가정하고 유의수준 0.05 하에서 검정)

- Urban변수에 따른 Sales의 차이를 통계적으로 검증하기 위한 독립표본 t-검정의 수행이 필요
  - 귀무가설: 도시인지에 따른 판매량에 차이가 없음
  - 대립가설: 도시 여부에 따른 판매량에 차이가 있음
- 독립표본 t 검정을 수행하기 앞서, 두 집단 간의 데이터 등분산성을 만족하는지 확인하기 위해 등분산 검정을 수행.

```R
var.test(Sales~Urban, data = Carseats, alternative='two.sided')

	F test to compare two variances

data:  Sales by Urban
F = 0.9787, num df = 117, denom df = 281, p-value = 0.9072
alternative hypothesis: true ratio of variances is not equal to 1
95 percent confidence interval:
 0.7276615 1.3423111
sample estimates:
ratio of variances 
         0.9786966
```

- 유의확률이 0.9072로 등분산성을 만족한다.

두 모집단이 등분산성 가정을 만족한다는 가정하에서 독립표본 t-검정을 실시

```R
t.test(Sales~Urban, data = Carseats, alternative='two.sided', var.equal=T)

	Two Sample t-test

data:  Sales by Urban
t = 0.30765, df = 398, p-value = 0.7585
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.5140440  0.7047797
sample estimates:
 mean in group No mean in group Yes 
         7.563559          7.468191 
```

- 유의확률이 0.7585로 귀무가설을 기각할 수 없기 때문에 도시인지에 따른 판매량의 차이는 존재하지 않는다고 결론 내릴 수 있음.

### 2) Sales변수와 CompPrice, Income, Advertising, Population, Price, Age, Education 간 변수들 간에 피어슨 상관계수를 이용한 상관관계를 분석을 수행하고 이를 해석하시오.

- 사전에 변수 사용을 쉽게하려고 `attach()`를 사용함.

```R
attach(Carseats)
# Sales, CompPrice
cor.test(Sales, CompPrice)

	Pearson''s product-moment correlation

data:  Sales and CompPrice
t = 1.281, df = 398, p-value = 0.2009
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 -0.03418779  0.16111814
sample estimates:
       cor 
0.06407873 
# 유의확률이 0.2009로 5% 유의수준에서 귀무가설을 기각할 수 없음

# Sales, Income
cor.test(Sales, Income)

	Pearson''s product-moment correlation

data:  Sales and Income
t = 3.067, df = 398, p-value = 0.00231
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.05471445 0.24633258
sample estimates:
     cor 
0.151951 
# 유의확률이 0.00231로 5% 유의수준에서 귀무가설을 기각함. 따라서 Sales와 Income은 양의 상관관계를 가짐

# Sales, Advertising
cor.test(Sales, Advertising)

	Pearson''s product-moment correlation

data:  Sales and Advertising
t = 5.5832, df = 398, p-value = 4.378e-08
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.1761088 0.3580956
sample estimates:
      cor 
0.2695068 
# 유의확률이 4.378e-08로 매우 작아 5% 유의수준에서 귀무가설을 기각함. 따라서 Sales와 Advertising은 서로 양의 상관관계를 가짐

# Sales, Population
cor.test(Sales, Population)

	Pearson''s product-moment correlation

data:  Sales and Population
t = 1.0082, df = 398, p-value = 0.314
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 -0.04781737  0.14779132
sample estimates:
       cor 
0.05047098
# 유의확률이 0.314로 5% 유의수준에서 귀무가설을 기각할 수 없음.

# Sales, Price
cor.test(Sales, Price)

	Pearson''s product-moment correlation

data:  Sales and Price
t = -9.912, df = 398, p-value < 2.2e-16
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 -0.5203026 -0.3627240
sample estimates:
       cor 
-0.4449507 
# 유의확률이 2.2e-16보다 작음 따라서 5% 유의수준에서 귀무가설을 기각할 수 있음. 따라서 Price와 Sale는 서로 음의 상관관계를 가짐
# 가격이 높아지면 판매량이 축소하는 경제논리를 따르고 있음

# Sales, Age
cor.test(Sales, Age)

	Pearson''s product-moment correlation

data:  Sales and Age
t = -4.7542, df = 398, p-value = 2.789e-06
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 -0.3225359 -0.1368749
sample estimates:
       cor 
-0.2318154 
# 유의확률이 2.789e-06로 5% 유의수준에서 귀무가설을 기각할 수 있음. 따라서 Sales와 Age는 서로 음의 상관관계를 가짐.

# Sales, Education
cor.test(Sales, Education)

	Pearson''s product-moment correlation

data:  Sales and Education
t = -1.0379, df = 398, p-value = 0.2999
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 -0.14924665  0.04633251
sample estimates:
        cor 
-0.05195524
# 유의확률이 0.2999로 5% 유의수준에서 귀무가설을 기각할 수 없음.
```

- Sales변수는 Income, Advertising 변수와는 양의 상관관계를 갖으나 그 값이 0.3보다 낮아 약한 양의 상관관계를 갖는다고 이야기할 수 있음. 또한 자동차 판매량과 소득과 홍보는 + 관계를 맺고 있음. 반면 Price와, Age의 경우 Sales와 음의 상관관계를 지니고 있음, 그 값이 각각 -0.44, -0.23으로 강한 음의 상관관계를 갖는다고 이야기 할 수 없음. 하지만, Price와, Age은 자동차 판매량과 - 관계를 갖고 있음

```R
cor(Carseats[,-c(7, 10, 11)])

                  Sales   CompPrice       Income  Advertising   Population       Price          Age    Education
Sales        1.00000000  0.06407873  0.151950979  0.269506781  0.050470984 -0.44495073 -0.231815440 -0.051955242
CompPrice    0.06407873  1.00000000 -0.080653423 -0.024198788 -0.094706516  0.58484777 -0.100238817  0.025197050
Income       0.15195098 -0.08065342  1.000000000  0.058994706 -0.007876994 -0.05669820 -0.004670094 -0.056855422
Advertising  0.26950678 -0.02419879  0.058994706  1.000000000  0.265652145  0.04453687 -0.004557497 -0.033594307
Population   0.05047098 -0.09470652 -0.007876994  0.265652145  1.000000000 -0.01214362 -0.042663355 -0.106378231
Price       -0.44495073  0.58484777 -0.056698202  0.044536874 -0.012143620  1.00000000 -0.102176839  0.011746599
Age         -0.23181544 -0.10023882 -0.004670094 -0.004557497 -0.042663355 -0.10217684  1.000000000  0.006488032
Education   -0.05195524  0.02519705 -0.056855422 -0.033594307 -0.106378231  0.01174660  0.006488032  1.000000000


plot(Carseats[,-c(7, 10, 11)])
```

### 3) 종속변수를 Sales, 독립변수를 CompPrice, Income, Advertising, Population, Price, Age, Education으로 설정하고 후진제거법을 활용하여 회귀분석을 실시하고 추정된 회귀식을 작성하시오.

- 바로 step함수를 사용하여 후진 제거법을 사용함.

```R
step(lm(Sales~CompPrice+Income+Advertising+Population+Price+Age+Education), 
     direction = 'backward')

Start:  AIC=533.5
Sales ~ CompPrice + Income + Advertising + Population + Price + 
    Age + Education

              Df Sum of Sq    RSS    AIC
- Population   1      0.12 1458.7 531.53
- Education    1      4.32 1462.9 532.68
<none>                     1458.6 533.50
- Income       1     51.03 1509.6 545.25
- Age          1    208.48 1667.0 584.94
- Advertising  1    278.65 1737.2 601.43
- CompPrice    1    533.98 1992.5 656.28
- Price        1   1247.94 2706.5 778.78

Step:  AIC=531.53
Sales ~ CompPrice + Income + Advertising + Price + Age + Education

              Df Sum of Sq    RSS    AIC
- Education    1      4.21 1462.9 530.68
<none>                     1458.7 531.53
- Income       1     51.29 1510.0 543.35
- Age          1    208.51 1667.2 582.97
- Advertising  1    295.91 1754.6 603.41
- CompPrice    1    540.75 1999.4 655.66
- Price        1   1250.06 2708.7 777.11

Step:  AIC=530.68
Sales ~ CompPrice + Income + Advertising + Price + Age

              Df Sum of Sq    RSS    AIC
<none>                     1462.9 530.68
- Income       1     53.02 1515.9 542.92
- Age          1    209.00 1671.9 582.10
- Advertising  1    298.27 1761.2 602.91
- CompPrice    1    539.21 2002.1 654.20
- Price        1   1249.81 2712.7 775.70

Call:
lm(formula = Sales ~ CompPrice + Income + Advertising + Price + 
    Age)

Coefficients:
(Intercept)    CompPrice       Income  Advertising        Price          Age  
    7.10919      0.09390      0.01309      0.13061     -0.09254     -0.04497 
```

- 가장 낮은 정보기준을 갖는 모형은 y = 7.10919 + 0.09390*CompPrice + 0.01309*Income + 0.13061*Advertising - 0.09254*Price - 0.04497*Age으로 최종 선택된다. 해당 모형을 따로 회귀분석을 진행하면

```R
car.lm = lm(formula = Sales ~ CompPrice + Income + Advertising + Price + Age)
summary(car.lm)

Call:
lm(formula = Sales ~ CompPrice + Income + Advertising + Price + 
    Age)

Residuals:
    Min      1Q  Median      3Q     Max 
-4.9071 -1.3081 -0.1892  1.1495  4.6980 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept)  7.109190   0.943940   7.531 3.46e-13 ***
CompPrice    0.093904   0.007792  12.051  < 2e-16 ***
Income       0.013092   0.003465   3.779 0.000182 ***
Advertising  0.130611   0.014572   8.963  < 2e-16 ***
Price       -0.092543   0.005044 -18.347  < 2e-16 ***
Age         -0.044971   0.005994  -7.503 4.20e-13 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 1.927 on 394 degrees of freedom
Multiple R-squared:  0.5403,	Adjusted R-squared:  0.5345 
F-statistic: 92.62 on 5 and 394 DF,  p-value: < 2.2e-16
```

- 모든 독립변수의 유의확률은 5% 유의수준에서 통계적으로 유의한 것을 확인할 수 있다.
- 본 모형을 통해 경쟁업체가 부과하는 가격이 높을수록, 지역 소득 수준이 높을수록, 각 지역의 광고예산이 높을수록, 자동차 좌석의 가격이 낮을수록, 인구 연령대가 낮을수록 판매량은 높아지는 것을 확인할 수 있다.

## 2️⃣ 정형 데이터 마이닝(사용 데이터: BlackFriday)

### 1) 'BlackFriday' 데이터에서 Product_Category_2, Product_Category_3의 NA 값을 0값으로 대체하고 Product_Category_1, 2, 3 변수의 값을 다 더한 Product_all 변수를 생성하여 추가하라. 그리고 User_ID를 character 변수로 , Occupation, Marital_Status, Product_category_1, Product_category_2, Product_category_3 변수를 범주형 변수로 변환하시오. 마지막으로 범주형 변수인 Gender, Age, City,_Category, Stay_In_Current_City_Years를 더 미변수로 변환해서 BlackFriday 데이터에 추가하시오.

```R
BF = read.csv('BlackFriday.csv')

str(BF)

# 문제의 요구대로 Product_Category_1, 2, 3에서 NA인 값을 0으로 대체했다. 
BF$Product_Category_1 = ifelse(is.na(BF$Product_Category_1), 0, BF$Product_Category_1)
BF$Product_Category_2 = ifelse(is.na(BF$Product_Category_2), 0, BF$Product_Category_2)
BF$Product_Category_3 = ifelse(is.na(BF$Product_Category_3), 0, BF$Product_Category_3)

# 그 이후에 Product_Category_1 ,2, 3을 다 더한 후 Product_all이란 변수를 BF에 추가했다.
Product_all = BF$Product_Category_1 + BF$Product_Category_2 + BF$Product_Category_3
BF[,'Product_all'] = Product_all


# User_ID를 Character 변수로 변환
BF$User_ID = as.character(BF$User_ID)

# Occupation factor 변수로 변환
BF$Occupation = factor(BF$Occupation)

# Marital_Status factor 변수로 변환
BF$Marital_Status = factor(BF$Marital_Status)

# 
BF$Product_Category_1 = factor(BF$Product_Category_1)
BF$Product_Category_2 = factor(BF$Product_Category_2)
BF$Product_Category_3 = factor(BF$Product_Category_3)

as.character(BF$Gender) = ifelse(as.character(BF$Gender) == 'M', 1, 0)
# Product_all이라는 변수를 BlackFriday 데이터에 Product_category_1, 2, 3 값을 모두 더해 추가했으며,
# User_ID를 character 변수로, Occupation, Martial_Status, Product_Category_1, Product_Category_2, Product_Category_3 변수를
# 범주형 변수로 각각 as.character(), factor() 함수로 데이터 유형을 변환함.
# str()함수를 통해 변수 변환을 확인할 수 있음.

# 더미화 진행을 위해 해당 변수에 대해 수치화한 후, caret패키지의 dummyVars를 활용하여 더미화를 진행.
# 더미화 Gender, Age, City_Category, Stay_In_Current_City_Years
# 더미화를 위해 해당 변수 수치화.

library(caret)
library(dplyr)

BF_1 = BF %>% mutate(Gender_binary = as.numeric(Gender),
                     age_binary = as.numeric(Age),
                     City_Category_numeric = as.numeric(City_Category),
                     Stay_In_Current_City_Years_numeric = as.numeric(Stay_In_Current_City_Years))


dummy = dummyVars("~ Gender + Age + City_Category + Stay_In_Current_City_Years", data = BF_1)
new_bf = data.frame(predict(dummy, newdata=BF_1))
BF_2 = cbind(BF, new_bf)
str(BF_2)
# 더미 변수화를 위해 caret 패키지의 dummyVars 함수를 활용. 더미화 진행을 위해 Gender, Age, City_Category, Stay_In_Current_City_Years
# 변수를 수치형 변수로 변환한 뒤 BF_1 데이터에 저장했다. dummyVars 함수를 통해 더미화 진행.
# 더미화된 변수는 리스트 형태로 나타나기 때문에 이를 data.frame 형태로 저장한 뒤, 열병합으로 BF_2로 저장
# str()함수로 데이터 구조 확인 -> 더미 변수가 추가됨.
```

### 2)  1)에서 전처리가 완료된 데이터에서 USE_ID, Product_ID, Gender, Age, City_Category, Stay_In_Current_City_Years, Product_all 변수를 제외한 나머지 변수들을 활용하여 kmeans 군집 분석을 수행하고 해석하시오.(범주형 변수를 수치형 변수로 변환하여 분석에 활용하시오.) 그리고 최적의 군집 개수를 찾아서 만일 군집 개수가 이전 결과와 다르면 분석을 다시 수행하여 해석하시오.

``` R
# 군집분석을 수행하기 위해 나머지 변수를 추가한 후, 범주형 변수는 수치형 변수로 변환
BF_cluster = BF_2 %>% select(-User_ID,
                             -Product_ID,
                             -Gender,
                             -Age,
                             -City_Category,
                             -Stay_In_Current_City_Years,
                             -Product_all)

BF_cluster$Occupation = as.numeric(BF_cluster$Occupation)
BF_cluster$Marital_Status = as.numeric(BF_cluster$Marital_Status)
BF_cluster$Product_Category_1 = as.numeric(BF_cluster$Product_Category_1)
BF_cluster$Product_Category_2 = as.numeric(BF_cluster$Product_Category_2)
BF_cluster$Product_Category_3 = as.numeric(BF_cluster$Product_Category_3)
str(BF_cluster)

# BF_cluster에 BF_2의 변수 중 해당 변수를 제외한 나머지 변수를 추가했음.
# Factor형 변수를 numeric 변수로 변환하기 위해 as.numeric()함수를 활용했음.
# str()함수로 구조를 확인한 결과 BF_cluster의 모든 변수가 수치형 변수로 변환되었음을 확인할 수 있음.

# kmeans 함수를 통해 군집분석을 실시

set.seed(1234)
kmeans_BF = kmeans(BF_cluster, 3)
kmeans_BF

# kmeans 함수를 활용해 kmeans clustering을 실시. 군집의 수는 3개로 지정했음(최적 군집의 수는 다음 분석에서 찾아볼 것임)
# 각 군집에 119245, 252697, 165635로 묶이게 되었음. between_SS / Total_SS의 값이 86%로 나타나 군집이 잘 형성되었음을 알 수 있음.

# sum of square means 그래프를 통해 최적의 군집을 찾아보자.

wssplot = function(data, nc = 15, seed=1234 ) {
  wss = (nrow(data)-1) * sum(apply(data, 2, var))
  for(i in 2:nc) {
    set.seed(seed)
    wss[i] = sum(kmeans(data, center=i)$withinss)
  }
  plot(1:nc, wss, type='b', xlab='Number of Clusters',ylab='within groups sum of squares')
}

wssplot(data = BF_cluster, nc=15, seed=1234)

# sum of square means plot을 통해 최적 군집의 수를 파악
# 급격하게 감소하는 군집의 수는 2~3이며 군집의 수 4부터 크게 감소하지 않음을 알 수 있음.
# 따라서 최적 군집의 수를 4로 지정하여 분석

kmeans_BF2 = kmeans(BF_cluster, center=4)
kmeans_BF2
# 각 군지의 원소는 109575, 89439, 106191, 232372개씩 나눠져 있으며
# (between_SS / total_SS =  91.9 %)로 3개로 군집했을 때 보다 더 잘 군집되어 있음을 알 수 있음.
```

![numbers of clustering](.\img\numbers of clustering.png)

### 3) 최적의 군집 개수를 찾아 재수행한 군집분석의 결과로 군집번호를 원본 데이터인 BF데이터의 각 행에 맞게 labeling하여 clust라는 변수로 저장하고 cluster별 특성을 파악하여 설명하시오.

```R
# 원본데이터에 분류된 결과를 각 행에 맞게 라벨링하여 clust 변수로 저장하여 csv 파일로 출력
Kmenas_cluster = kmeans_BF2$cluster
BF_full = cbind(BF, clust=Kmenas_cluster)
str(BF_full)

write.csv(BF_full, 'BlackFriday clust.csv')

# 군집의 개수를 4개로 하여 해당 cluster 분류를 열병합하여 BF_full 데이터에 저장함. str()함수를 통해 구조를 보면
# clust 변수가 추가되었음을 알 수 있음.
# 이후 write.csv 데이터를 csv로 출력함.


# table 함수를 통해 군집 내 개수를 파악하고 xlabs 함수를 통해 군집별 특성을 파악.
table(BF_full$clust)

# cluster 별 Gender 요약
xtabs(BF_full$clust ~ BF_full$Gender)

xtabs(~BF_full$clust + BF_full$Gender)
# 먼저 clust 개수를 파악하기 위해 table 함수를 파악, 2>3>1>4 번 군집 순으로 군집이 묶여있음을 알 수 있음. clust별 Gender를 요약할 때,
# xtabs 함수를 사용함. 전체 성비를 확인한 결과 Female은 394576이며, Male은 1141938임. 즉 Male이 3배 많음을 알 수 있음.
# clust별 Gender를 확인한 결과 모든 clust에서 Male의 수가 압도적으로 많으며, 비율의 차이가 가장 많이 나는 군집은 1번 군집으로 파악됨.

# clust별 Age 요약
xtabs(BF_full$clust ~ BF_full$Age)

xtabs(~BF_full$clust + BF_full$Age)

# 전체의 연령대를 확인한 결과, '26~35'가 613010로 가장 많았으며, 다음은 36-45, 18-25, 46-50, 51-55, 55+, 0-17 순으로 나타났다.
# 또한 clust별 age를 확인한 결과 모든 군집에서 26-35가 많음을 알 수 있으며 4번 군집을 제외하고 전체 연령대는 대부분 거의 변동이 나타나지 않았다.



# Clust별 Purchase 요약
aggregate(Purchase~clust, BF_full, mean)

# Purchase별 Age 요약
aggregate(Purchase~Age, BF_full, mean)

# Purchase별 Gender 요약
aggregate(Purchase~Gender, BF_full, mean)

# clust별 Purchase를 확인한 결과 1번 군집의 평균 물건 구매 값이 가장 높게 나타났으며, 3>4>2번 순으로 평균가격이 높음을 알 수 있다.
# Age별 Purchase를 확인한 결과 모든 연령에서 큰 차이를 보이진 않으나 51~55 연령에서 가장 많은 지출을 하고 있음을 알 수 있다.
# 마지막으로 Gender별 Purchase를 확인하면 Female보다는 male이 평균적으로 보다 지출을 많이 하고 있음을 알 수 있다.
```

## 3️⃣ 비정형 데이터마이닝(사용데이터: 공구블로그 댓글)

### 공구 블로그 댓글.txt 데이터는 공구구매와 관련된 블로그에 댓글에 대한 자료이며, "사전.txt"는 댓글에 언급된 제품명이 들어있는 사전이다.

### 1) 공구 블로그 댓글.txt 파일을 읽고 숫자, 특수문자 등을 제거하는 전처리 작업을 시행하시오.

```R
gonggu = read.csv('공구 블로그 댓글.txt', sep="\t") 
str(gonggu)
summary(gonggu)

gonggu$Date = substr(gonggu$Date, 1, 10) # 읽어오니 '\t'가 있었음. 제거를 위해 strsub를 사용

gonggu$Content = as.character(gonggu$Content) # 해당 데이터 열이 factor형인 것을 확인 문자열로 변형

# 필요 패키지 로드
library(stringr)
library(rJava)
library(tm)
library(KoNLP)
library(plyr)
library(wordcloud)

useSejongDic() # 사용할 사전 로드

clean_txt = function(txt) { # 1) 문제에서 요구한 텍스트 데이터 전처리를 위한 함수
  txt = tolower(txt) # 대문자를 소문자로
  txt = removeNumbers(txt) # 숫자 제거
  txt = stripWhitespace(txt) # 공백제거
  txt = removePunctuation(txt) # 구두점 제거
  
  return(txt)
}

gonggu$Content = clean_txt(gonggu$Content) # 전처리 수행
```

### 2) 사전.txt를 사전에 추가하고 문서에서 형용사를 추출하여라.

```R
buildDictionary(ext_dic = 'woorimalsam', user_dic=data.frame(readLines('사전.txt'), 'ncn'), replace_usr_dic=T) # 사전.txx를 사전에 추가

doc = as.character(gonggu$Content) # 형용사를 추출를 위한 준비 -> 위에서 해줘서 사실 필요가 없음
pos = paste(SimplePos09(doc)) # 형용사 추출을 위해 구분을 지음
extracted = str_match(pos, '([가-힣]+)/[P]') # 정규표현식을 사용한 형용사 추출, P가 있으면 형용사임
keyword = extracted[, 2] # 해당 형용사 추출
keyword[!is.na(keyword)] # NA부분을 제외한 나머지 추출
# 부탁드리라는 표현이 가장 많이 보임
```

### 3) 2월에 게시된 댓글의 명사를 추출하고 빈도수를 시각화하시오.

```R
# 2월 추출
gonggu$Date = as.factor(gonggu$Date) # Date형식으로 맞춰줘야하는데, strsub() 함수를 사용하고 난 뒤에는 문자형으로 출력되어 있음. 문자형은 Date로 표현이 불가능하니 factor로 맞춰줌
gonggu$Date = as.Date(gonggu$Date, format="%Y.%m.%d") # 날짜 표현식으로 Date 형식으로 맞춤
gonggu$month = as.numeric(format(gonggu$Date, '%m')) # 그리고 이 중 month인 부분만 따로 추출
gonggu$month # 확인
gonggu2 = subset(gonggu, gonggu$month == 2) # 여기서 2월인 부분만 따로 데이터 셋을 만듬

# 2월 댓글 명사 추출
gonggu_exN = sapply(gonggu2$Content, extractNoun) # 명사 추출
Noun = as.vector(unlist(gonggu_exN)) # 벡터로 통합
Noun_2 = Noun[nchar(Noun)>=2] # 최소 2번 이상 등장한 명사만 추출
table.cnoun = head(sort(table(Noun_2), decreasing = T), 5) # 상위 5개 명사만 추출

colors = rainbow(5) # 5개의 색상 결정
barplot(table.cnoun, main="2월 댓글 빈출 명사", col=colors) # Barplot으로 시각화
legend("right", names(table.cnoun), fill=colors) # legend로 범례 맞춰주기
```

![2월 댓글 빈출 명사](img/2월 댓글 빈출 명사.png)