# Title

## Abstract

## Introduction

I started to record what I ate everyday in July 2022 by a very
incidental chance. Since then, I spent most of my time in Hong Kong
until I moved to Austin in July 2023. When I was in HK, I was wondering
whether people tend to eat better (to relax or compensate) or simpler
(to save time) when they are busy. However, my life and food patterns in
HK were so complicated and unpredictable to verify this hypothesis.

Considering the feasibility, I decide to estimate and predict my life
and food patterns in Austin. I am not very confident in the predictive
accuracy for two reasons. First, although my life in Austin is simple
due to some constraints, the data is from real human with certain
flexibility and unpredictability. Second, the data set is small.
However, it is still fun to know the driving factors of my life and food
patterns.

## Methods

### Data wrangling

To implement this, I filter relevant `date` in Austin: after Jul 4, 2023
(inclusive), exclude Thanksgiving holiday (from Nov 20 to Nov 26, both
inclusive) and winter vacation (from Dec 12, 2023 to Jan 11, 2024, both
inclusive).

During this time, I am studying at University of Texas at Austin, so my
life pattern heavily depends on the school calender. Thus, I create a
`semester` variable: it equals to “summer” when `date` is before Aug 14
(inclusive), equals to “fall” when `date` is after Aug 15 and before Dec
11 (both inclusive), and equals to “spring” otherwise.

Create `week_of_sem` column

## Check spring break

Below is the data frame:

    ## # A tibble: 6 × 7
    ##   dow   semester week_of_sem meal   food_class breakfast_or_not
    ##   <fct> <fct>    <fct>       <fct>  <fct>      <fct>           
    ## 1 Wed   summer   0           lunch  other      1               
    ## 2 Thu   summer   0           lunch  other      1               
    ## 3 Fri   summer   0           dinner other      0               
    ## 4 Sat   summer   0           lunch  home       0               
    ## 5 Sat   summer   0           dinner home       0               
    ## 6 Sun   summer   0           lunch  home       1               
    ## # ℹ 1 more variable: days_since_last_meal <dbl>

    ## # A tibble: 3 × 2
    ## # Groups:   food_class [3]
    ##   food_class count
    ##   <fct>      <int>
    ## 1 canteen       86
    ## 2 home         204
    ## 3 other         63

## Results

## Conclusion
