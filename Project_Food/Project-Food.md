# Title

I started to record what I ate everyday in July 2022 by a very
incidental chance. Since then, I spent most of my time in Hong Kong
until I moved to Austin in July 2023. When I was in HK, I was wondering
when people are busy, do they tend to eat better (to relax or
compensate) or simpler (to save time)? However, my life and food
patterns in HK were so complicated and unpredictable.

Considering the feasibility, I decide to estimate and predict my life
and food patterns in Austin. I am not very confident in the predictive
accuracy considering two reasons. First, although my life in Austin is
simple due to some constraints, the data is from real human with certain
flexibility and unpredictability. Second, the data set is small.
However, it is still fun to know the driving factors of my life and food
patterns.

To implement this, I filter relevant `date` in Austin: keep
`date >= 2023-07-04`, exclude Thanksgiving holiday (`date` in
\[2023-11-20, 2023-11-26\]) and winter vacation (`date` in
\[2023-12-12,2024-01-11\]).

I am studying at University of Texas at Austin, so my life pattern
heavily depends on the school calender. Thus, I create a `semester`
variable: it equals to “summer” when `date <= 2023-08-14`, equals to
“fall” when `date` in \[2023-08-14, 2023-12-11\], and equals to “spring”
otherwise.

Create `week_of_sem` column

## Check spring break

Below is the data frame:

    ##         date dow           breakfast               lunch       dinner semester
    ## 1 2023-07-04 Tue                <NA>    SouthCloud Ramen         <NA>   summer
    ## 2 2023-07-05 Wed MA Econ orientation MA Econ orientation         <NA>   summer
    ## 3 2023-07-06 Thu                Home             Wendy's         <NA>   summer
    ## 4 2023-07-07 Fri                <NA>                Home China Family   summer
    ## 5 2023-07-08 Sat                <NA>                Home         Home   summer
    ## 6 2023-07-09 Sun                Home                Home         <NA>   summer
    ##   week_of_sem
    ## 1           0
    ## 2           0
    ## 3           0
    ## 4           0
    ## 5           0
    ## 6           0

Convert wide data to long data  
Drop N/A in `food`

    ## # A tibble: 6 × 7
    ##   date       dow   breakfast           semester week_of_sem meal   food         
    ##   <date>     <chr> <chr>               <chr>          <int> <chr>  <chr>        
    ## 1 2023-07-04 Tue   <NA>                summer             0 lunch  SouthCloud R…
    ## 2 2023-07-05 Wed   MA Econ orientation summer             0 lunch  MA Econ orie…
    ## 3 2023-07-06 Thu   Home                summer             0 lunch  Wendy's      
    ## 4 2023-07-07 Fri   <NA>                summer             0 lunch  Home         
    ## 5 2023-07-07 Fri   <NA>                summer             0 dinner China Family 
    ## 6 2023-07-08 Sat   <NA>                summer             0 lunch  Home

Create 2 categorical columns using `case_when`  
Create a column, the difference in `date` between this observation and
the last observation with the same `food_class`

    ## # A tibble: 6 × 10
    ##   date       dow   breakfast         semester week_of_sem meal  food  food_class
    ##   <date>     <chr> <chr>             <chr>          <int> <chr> <chr> <chr>     
    ## 1 2023-07-04 Tue   <NA>              summer             0 lunch Sout… other     
    ## 2 2023-07-05 Wed   MA Econ orientat… summer             0 lunch MA E… other     
    ## 3 2023-07-06 Thu   Home              summer             0 lunch Wend… other     
    ## 4 2023-07-07 Fri   <NA>              summer             0 lunch Home  home      
    ## 5 2023-07-07 Fri   <NA>              summer             0 dinn… Chin… other     
    ## 6 2023-07-08 Sat   <NA>              summer             0 lunch Home  home      
    ## # ℹ 2 more variables: breakfast_or_not <dbl>, days_since_last_eat <dbl>

Drop N/A in `days_since_last_eat` (First meal of a `food_class`)  
Select columns  
Convert data type of several columns

    ## # A tibble: 6 × 7
    ##   dow   semester week_of_sem meal   food_class breakfast_or_not
    ##   <fct> <fct>    <fct>       <fct>  <fct>      <fct>           
    ## 1 Wed   summer   0           lunch  other      1               
    ## 2 Thu   summer   0           lunch  other      1               
    ## 3 Fri   summer   0           dinner other      0               
    ## 4 Sat   summer   0           lunch  home       0               
    ## 5 Sat   summer   0           dinner home       0               
    ## 6 Sun   summer   0           lunch  home       1               
    ## # ℹ 1 more variable: days_since_last_eat <dbl>

    ## # A tibble: 3 × 2
    ## # Groups:   food_class [3]
    ##   food_class count
    ##   <fct>      <int>
    ## 1 canteen       86
    ## 2 home         204
    ## 3 other         63
