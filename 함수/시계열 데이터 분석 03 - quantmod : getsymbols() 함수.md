# 🕑 quantmod : getSymbols() 함수  

***  

<br>  

quantmod 패키지의 getSymbols( ) 함수를 통해 야후 파이낸스 데이터를 ts data 형태로 불러올 수 있습니다.  

주말도 알아서 제외해줍니다.  

🕑 getSymbols( ) 함수 예시 : `getSymbols("META", src = "yahoo", from = as.Date("2015-08-01"), to = as.Date("2016-08-31"))`  



<br>  

``` r
## quantmod
## 페이스북 데이터 불러옴
## FB에서 META로 이름이 바뀌었으므로 META로 키값 지정

install.packages("quantmod")
library(quantmod)

getSymbols("META", src = "yahoo", from = as.Date("2015-08-01"), to = as.Date("2016-08-31"))
```
    >>
    
    ## [1] "META"  
    
<br>  

``` r
## 트위터 데이터 불러옴

getSymbols("TWTR", src = "yahoo", from = as.Date("2015-08-01"), to = as.Date("2016-08-31"))
```
    >>
    
    ## [1] "TWTR"  
    
<br>  

***  
