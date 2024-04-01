## What causes what?

1.  Crime and police is a pair of simultaneity. More crime causes more
    police, but meanwhile more police causes less crime. Regressing
    crime on police cannot identify the causal effect of police on
    crime.

2.  The researchers used terrorism alert level as an instrumental
    variable. On high terrorist alert days, there were more police
    neglecting the level of street crime.  
    Regression results: The total number of crimes in D.C. decreased by
    7.316 on a high alert day. Controlling for Metro ridership, the
    total number of crimes in D.C. decreased by 6.046 on a high alert
    day.

3.  They wanted to know whether the decrease in crime was caused by
    fewer victims on high alert days. Metro ridership captures the
    number of victims.

4.  
    crime = *β*<sub>0</sub> + *β*<sub>1</sub> × High Alert × District 1 + *β*<sub>2</sub> × High Alert × Other Districts + *β*<sub>3</sub> × log (midday ridership) + *u*
      
    In the first police district area (District 1 = 1), the total number
    of crimes decreased by 2.621 on high alert days (High Alert = 1). In
    other districts, the total number of crimes did not significantly
    change on high alert days.

## Tree modeling: dengue cases

I use *CART*, *random forests*, and *gradient-boosted trees* to predict
dengue cases.

I split data into training set and test set.

I include all features in CART. I use 10-fold cross validation on the
training set to find the optimal complexity parameter.

I include all features in random forest.

I include all features in gradient-boosted trees. I manually tune
several parameters.

Out-of-sample RMSE:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">Model</th>
<th style="text-align: right;">RMSE</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">CART</td>
<td style="text-align: right;">25.82233</td>
</tr>
<tr class="even">
<td style="text-align: left;">Random forest</td>
<td style="text-align: right;">21.92378</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gradient-boosted trees</td>
<td style="text-align: right;">22.24624</td>
</tr>
</tbody>
</table>

Random forest performs best with the lowest RMSE.

Partial dependence plots of random forest:
![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots-1.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots-2.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots-3.png)

## Predictive model building: green certification

## Predictive model building: California housing
