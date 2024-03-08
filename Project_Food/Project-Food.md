# Title

I started to record what I ate everyday in July 2022 by a very
incidental chance. Since then, I spent most of my time in Hong Kong
until I moved to Austin in July 2023. When I was in HK, I was wondering
when people are busy, do they tend to eat better (to relax or
compensate) or simpler (to save time)? However, my life and food
patterns in HK were so complicated and unpredictable.

Considering the feasibility, I focus on my life in Austin. To implement
this, I keep `date >= 2023-07-04`, exclude Thanksgiving holiday
`2023-11-20 <= date <= 2023-11-26` and winter vacation
`2023-12-12 <= date <= 2024-01-11`.

Create `semester` column: = “summer” when `date` &lt;= 2023-08-14; =
“fall” when `date` &lt;= 2023-12-11; “spring” otherwise.  
Create `week_of_sem` column \## Check spring break

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

    ## # A tibble: 6 × 7
    ##   date       dow   breakfast           semester week_of_sem meal   food         
    ##   <date>     <chr> <chr>               <chr>          <int> <chr>  <chr>        
    ## 1 2023-07-04 Tue   <NA>                summer             0 lunch  SouthCloud R…
    ## 2 2023-07-05 Wed   MA Econ orientation summer             0 lunch  MA Econ orie…
    ## 3 2023-07-06 Thu   Home                summer             0 lunch  Wendy's      
    ## 4 2023-07-07 Fri   <NA>                summer             0 lunch  Home         
    ## 5 2023-07-07 Fri   <NA>                summer             0 dinner China Family 
    ## 6 2023-07-08 Sat   <NA>                summer             0 lunch  Home

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
