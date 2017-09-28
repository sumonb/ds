# BarChart
Sumon Barua  



Examples were taken from the book: 

* Graphics Cookbook: Practical Recipes for Visualizing Data
* Cookbook for R


Bar graph typically used to display:

* Numeric values (on the y-axis)
* Categories (on the x-axis)

####Heights of bars 

* The count of cases for each group - stat_count - stat="count"
* The value of a column - stat_identity - stat="identity"


```r
#install.packages("gcookbook")
library(gcookbook)
library(ggplot2)
pg_mean
```

```
##   group weight
## 1  ctrl  5.032
## 2  trt1  4.661
## 3  trt2  5.526
```

```r
ggplot(pg_mean, aes(x=group, y=weight)) + 
  geom_bar(stat="identity")
```

![](BarChart_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

When x is a continuous (or numeric) variable vs discrete (categorical variable with factor())

```r
BOD
```

```
##   Time demand
## 1    1    8.3
## 2    2   10.3
## 3    3   19.0
## 4    4   16.0
## 5    5   15.6
## 6    7   19.8
```

```r
#continuous
ggplot(BOD, aes(x=Time, y=demand)) + 
  geom_bar(stat="identity")
```

![](BarChart_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
#discrete
ggplot(BOD, aes(x=factor(Time), y=demand)) + 
  geom_bar(stat="identity")
```

![](BarChart_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

####Colouring - 

* fill - to fill the bars
* colour - bar outline color

```r
pg_mean
```

```
##   group weight
## 1  ctrl  5.032
## 2  trt1  4.661
## 3  trt2  5.526
```

```r
ggplot(pg_mean, aes(x=group, y=weight)) +
  geom_bar(stat="identity", fill="lightblue", colour="black")
```

![](BarChart_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

####Grouping bars together

* Map a variable to fill
* Use geom_bar(position="dodge")


```r
cabbage_exp
```

```
##   Cultivar Date Weight        sd  n         se
## 1      c39  d16   3.18 0.9566144 10 0.30250803
## 2      c39  d20   2.80 0.2788867 10 0.08819171
## 3      c39  d21   2.74 0.9834181 10 0.31098410
## 4      c52  d16   2.26 0.4452215 10 0.14079141
## 5      c52  d20   3.11 0.7908505 10 0.25008887
## 6      c52  d21   1.47 0.2110819 10 0.06674995
```

```r
ggplot(cabbage_exp, aes(x=Date, y=Weight, fill = Cultivar )) +
  geom_bar(stat = "identity", position = "dodge")
```

![](BarChart_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

####Custom colour palette
To set the colors, cale_fill_brewer() or scale_fill_manual() can be used

```r
cabbage_exp
```

```
##   Cultivar Date Weight        sd  n         se
## 1      c39  d16   3.18 0.9566144 10 0.30250803
## 2      c39  d20   2.80 0.2788867 10 0.08819171
## 3      c39  d21   2.74 0.9834181 10 0.31098410
## 4      c52  d16   2.26 0.4452215 10 0.14079141
## 5      c52  d20   3.11 0.7908505 10 0.25008887
## 6      c52  d21   1.47 0.2110819 10 0.06674995
```

```r
ggplot(cabbage_exp, aes(x=Date, y=Weight, fill=Cultivar)) +
   geom_bar(stat = "identity", position="dodge", colour="black") +
   scale_fill_brewer(palette="Pastel1")
```

![](BarChart_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


####Bar graph with count

```r
diamonds
```

```
## # A tibble: 53,940 x 10
##    carat       cut color clarity depth table price     x     y     z
##    <dbl>     <ord> <ord>   <ord> <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  0.23     Ideal     E     SI2  61.5    55   326  3.95  3.98  2.43
##  2  0.21   Premium     E     SI1  59.8    61   326  3.89  3.84  2.31
##  3  0.23      Good     E     VS1  56.9    65   327  4.05  4.07  2.31
##  4  0.29   Premium     I     VS2  62.4    58   334  4.20  4.23  2.63
##  5  0.31      Good     J     SI2  63.3    58   335  4.34  4.35  2.75
##  6  0.24 Very Good     J    VVS2  62.8    57   336  3.94  3.96  2.48
##  7  0.24 Very Good     I    VVS1  62.3    57   336  3.95  3.98  2.47
##  8  0.26 Very Good     H     SI1  61.9    55   337  4.07  4.11  2.53
##  9  0.22      Fair     E     VS2  65.1    61   337  3.87  3.78  2.49
## 10  0.23 Very Good     H     VS1  59.4    61   338  4.00  4.05  2.39
## # ... with 53,930 more rows
```

```r
ggplot(diamonds, aes(x=cut)) +
   geom_bar(stat = "count")
```

![](BarChart_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

####Custom colour
Custom colours can be used with help of scale_fill_manual

```r
upc <- subset(uspopchange, rank(Change)>40)
upc
```

```
##             State Abb Region Change
## 3         Arizona  AZ   West   24.6
## 6        Colorado  CO   West   16.9
## 10        Florida  FL  South   17.6
## 11        Georgia  GA  South   18.3
## 13          Idaho  ID   West   21.1
## 29         Nevada  NV   West   35.1
## 34 North Carolina  NC  South   18.5
## 41 South Carolina  SC  South   15.3
## 44          Texas  TX  South   20.6
## 45           Utah  UT   West   23.8
```

```r
ggplot(upc, aes(x= Abb , y = Change, fill = Region)) +
 geom_bar(stat="identity") +
 scale_fill_manual(values=c("#ef98aa", "#c2e3ec")) +
 xlab("State")
```

![](BarChart_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

```r
#Sort data
ggplot(upc, aes(x= reorder(Abb,Change) , y = Change, fill = Region)) +
 geom_bar(stat="identity") +
 scale_fill_manual(values=c("#ef98aa", "#c2e3ec")) +
 xlab("State")
```

![](BarChart_files/figure-html/unnamed-chunk-7-2.png)<!-- -->
