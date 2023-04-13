# 🕑 시계열 자료 plot  

<br>  


🕑 `plot()` : 원래는 x축, y축의 이름을 모두 정의해줘야 plot해주지만, y축에 관한 정보만 줘도 plot 해줍니다.  


<br>  

***  

<br>  


``` r 
## 데이터 선언

unemploy.df=read.csv("BOK_unemployment_rate.csv")
oil.df=read.csv("BOK_energy_oil.csv")
exchange.df=read.csv("BOK_exchange_rate_krw_usd.csv") 

unemploy.ts=ts(unemploy.df$unemployment_rate, start=2000, frequency=1)
oil.ts=ts(oil.df$oil, start=c(1994,1), frequency=12)
exchange.ts=ts(exchange.df$exchange_rate_krw_usd, start=c(1980,1), frequency=4)

getSymbols("META",src="yahoo", from = as.Date("2015-08-01"), to = as.Date("2016-08-31"))
```  
    
<br>  

``` r
par(mfrow=c(2,2))
plot(META$META.Adjusted,xlab="Time(Daily)",ylab="Adjusted Price", main="Facebook")
plot(oil.ts,xlab="Time(Monthly)",ylab="Petrolem consumption", main="Korean energy Petroleum consumption")
plot(exchange.ts,xlab="Time(Quarterly)",ylab="Exchange rate", main="Exchange Rate KRW per USD")
plot(unemploy.ts,xlab="Time(Yearly)",ylab="Unemployment rate", main="Korean unemployment rate")
```

![image](https://user-images.githubusercontent.com/65170165/225848863-c771a409-132d-4e72-bd18-da172bb1d586.png)

<br>  



<br>  

## 🕑 같은 time period의 두개의 변수움직임 비교하기  

<br>  

두 지표가 하나의 플롯에 출력됩니다.  

보통 옆으로 붙이는 것보다 위아래로 두고 비교하는 것이 눈에 더 잘보입니다만, start와 end 가 맞아야 비교에 의미가 있습니다.  

시간의 흐름에 대한 거시경제지표를 파악하기도 편합니다.  

<br>  


``` r
plot(economic.ts)
```

![image](https://user-images.githubusercontent.com/65170165/225849173-544e1d26-6186-41d5-9198-b20ce7e55a1a.png)  


<br>  



<br>  


## 🕑 위아래로 플롯  


<br>  

🕑 `par(mfrow = c(row, col))` 의 인수를 조정해서 위치를 정해줍니다.  

<br>  

``` r
par(mfrow=c(2,1))
plot(employment.ts, col="blue", lwd=2, ylab="Rate %", main="Monthly employment rate")
plot(bonds.ts, col="red", lwd=2, ylab="bonds 3 years(Year%)", main="Treasuray bond 3 years")
```

![image](https://user-images.githubusercontent.com/65170165/225849314-5dcb7f1e-671b-48be-a1b6-d1be576fbd4b.png)  

<br>  



<br>  

## 🕑 양옆으로 출력  

<br>  

🕑 `par(mfrow = c(row, col))` 의 인수를 조정해서 위치를 정해줍니다.  

<br>  


``` r
par(mfrow=c(1,2))
plot(economic.ts[,1], col="blue", lwd=2, ylab="Rate %", main="Monthly employment rate")
plot(economic.ts[,2], col="red", lwd=2, ylab="bonds 3 years(Year%)", main="Treasuray bond 3 years")
```

![image](https://user-images.githubusercontent.com/65170165/225849537-a5836937-d0ab-42fc-9e17-eb53d21e8a85.png)

<br>  



<br>   

## 🕑 두개의 시계열 옆으로 합치기  

<br>  

🕑 `cbind( ) 함수` 를 사용해 두개의 시계열 옆으로 합칩니다. 단, 두 자료가 동기간이며 주기 역시 동일해야 합니다.  


<br>  

``` r
two.ts=cbind(facebook.ts,twitter.ts)
head(two.ts)
```
    >>
    
    ##      facebook.ts twitter.ts
    ## [1,]       89.43      27.79
    ## [2,]       89.90      26.94
    ## [3,]      101.97      28.46
    ## [4,]      104.24      25.40
    ## [5,]      104.66      23.14
    ## [6,]      112.21      16.80  
    
<br>  

``` r
par(mfrow=c(1,1))
plot(two.ts, col="blue", lwd=2, ylab="",main="Adjusted close")
```

![image](https://user-images.githubusercontent.com/65170165/225849713-51bb20ed-411f-4e40-9c1c-e8210d10fe0a.png)  

<br>   

``` r
## 하나의 플롯에 출력
plot(two.ts, plot.type="single")
```

![image](https://user-images.githubusercontent.com/65170165/225849819-846a86d0-960b-42f8-b537-9ab6a8b8b502.png)

<br>  

<br>  


## 🕑 single 옵션  

<br>  

두 시계열 자료를 하나의 plot 안에서 나타내줍니다.  

time 축 및 y축을 공유해서 나타냅니다.  


두 축을 모두 공유하기 때문에, 두 자료의 y축 범위가 비슷해야만 그 차이를 제대로 볼 수 있습니다.  


두 지표가 있는 하나의 ts 데이터로 plot하는 경우에 주로 사용합니다.  

<br>  

``` r
plot(two.ts, plot.type="single",
     main="Monthly closing prices on Facebook and Twitter using plot()",ylab="Adjusted close price",col=c("blue", "red"), lty=1:2) 
     
legend("right", legend=c("Facebook","Twitter"), col=c("blue", "red"),lty=1:2)
```

![image](https://user-images.githubusercontent.com/65170165/225849904-c8e0e434-4bbd-4c2e-9a3c-d64c81c243cd.png)  

<br>  

<br>  


## 🕑 두 가지 ts 데이터로 플롯하기  

<br>  

ts 데이터는 ts.plot() 함수 사용이 가능합니다.  

🕑 `ts.plot(ts_DATA_1, ts_DATA_2, ...)`  

🕑 이 경우 single 옵션이 없어도 시간축과 y축의 범위를 맞춰줍니다.  



<br>  

``` r
ts.plot(facebook.ts, twitter.ts, col=c("blue", "red"), 
        main="Monthly closing prices on Facebook and Twitter using ts.plot()",ylab="Adjusted close price", lty=1:2)
        
legend("right", legend=c("Facebook","Twitter"), col=c("blue", "red"),lty=1:2)
```

![image](https://user-images.githubusercontent.com/65170165/225850020-53611764-768d-4e66-b6f5-f9d1428090e9.png)  

<br>  



<br>  

## 🕑 Chartseries 함수  

<br>  

앞선 글에서도 살펴보았듯이, quantmod로 가져온 데이터 chartSeries 함수를 사용해 plot할 수 있습니다.  

<br>  

``` r
#7.finance data from yahoo finance - Chartseries 
getSymbols("META",src="yahoo", from = as.Date("2015-08-01"), to = as.Date("2016-08-31"))
```
    >>
    
    ## [1] "META"  
    
<br>  

``` r
getSymbols("TWTR",src="yahoo", from = as.Date("2015-08-01"), to = as.Date("2016-08-31"))
```
    >>
    
    ## [1] "TWTR"  
    

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

<br>  
