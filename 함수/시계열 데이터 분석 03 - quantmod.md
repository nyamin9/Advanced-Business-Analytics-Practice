# 🕑 quantmod 패키지  

<br>  


## 🕑 getSymbols() 함수  

<br>  

quantmod 패키지의 getSymbols( ) 함수를 통해 야후 파이낸스 데이터를 ts data 형태로 불러올 수 있습니다.  

주말도 알아서 제외해줍니다.  

<br>  


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

<br>  

## 🕑 Chartseries 함수 

<br>  

quantmod를 사용해서 불러온 ts 데이터는 chartSeries( ) 함수를 통해 plot할 수 있습니다.  

<br>  

🕑 chartSeries( ) 함수 : `chartSeries(ts_DATA, theme)`  

<br>  

``` r
## ts 데이터 -> chartSeries 함수
chartSeries(META$META.Adjusted)
```  


![image](https://user-images.githubusercontent.com/65170165/225850136-5a255925-0cc8-49ff-8345-9666912df65a.png)  

<br>  

``` r
chartSeries(META$META.Adjusted, theme="white")
```

![image](https://user-images.githubusercontent.com/65170165/225850232-5359b371-2b18-4ba3-9da7-9d010fa2859d.png)  

<br>  

``` r
chartSeries(TWTR$TWTR.Adjusted, theme="white")
```

![image](https://user-images.githubusercontent.com/65170165/225850325-20e87552-dfc7-49b3-9648-d92a9a18864b.png)  

<br>

``` r
chartSeries(META, theme="white")
```

![image](https://user-images.githubusercontent.com/65170165/225850578-3541812e-c606-48cf-8b14-8235db0f3220.png)  


<br>

``` r
chartSeries(TWTR, theme="white")
```

![image](https://user-images.githubusercontent.com/65170165/225850663-a3f45c86-c046-4329-afb6-d62ff540b0ee.png)  

<br>    

***  
