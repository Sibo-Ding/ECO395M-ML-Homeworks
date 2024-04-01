This file takes 5 minutes to knit. Chunks `Random forest 2` and
`Random forest 3` take some time to run.

## What causes what?

1.  Crime and police is a pair of simultaneity. More crime causes more
    police, but meanwhile more police causes less crime. Regressing
    crime on police cannot identify the causal effect of police on
    crime.

2.  The researchers used terrorism alert level as an instrumental
    variable. On high terrorist alert days, there were more police
    neglecting the level of street crime. Then, they could estimate the
    causal effect of “extra” police on crime on those days.  
    Regression results: The daily number of crimes in D.C. decreased by
    7.316 on high alert days. Controlling for Metro ridership, the daily
    number of crimes in D.C. decreased by 6.046 on high alert days.

3.  The researchers wanted to know whether the decrease in crime was
    caused by fewer victims on the street on high alert days (as they
    were scared to go out). Metro ridership captures the number of
    victims.

4.  
    crime = *β*<sub>0</sub> + *β*<sub>1</sub> × High Alert × District 1 + *β*<sub>2</sub> × High Alert × Other Districts + *β*<sub>3</sub> × log (midday ridership) + *u*
      
    In the first police district area (District 1 = 1), the daily number
    of crimes decreased by 2.621 on high alert days (High Alert = 1). In
    other districts, the daily number of crimes did not significantly
    change on high alert days.

## Tree modeling: dengue cases

I use *CART*, *random forests*, and *gradient-boosted trees* to predict
dengue cases. The outcome variable is continuous, so it is a regression
problem. I convert `city` and `season` from strings to categories.

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
<td style="text-align: right;">27.97</td>
</tr>
<tr class="even">
<td style="text-align: left;">Random forest</td>
<td style="text-align: right;">21.92</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gradient-boosted trees</td>
<td style="text-align: right;">22.25</td>
</tr>
</tbody>
</table>

Random forest performs best with the lowest RMSE 21.92.

Partial dependence plots of 3 variables in the random forest model:
![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%201-1.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%201-2.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%201-3.png)

## Predictive model building: green certification

I want to predict rental revenue per square foot per calendar year for
commercial properties in the US. The outcome variable is continuous, so
it is a regression problem. I calculate revenue per foot year as the
product of `Rent` and `leasing_rate`. After that, I drop `Rent`,
`leasing_rate` and two identifiers.

I convert 8 features from continuous to categorical, which are
`renovated`, `class_a`, `class_b`, `LEED`, `Energystar`, `green_rating`,
`net`, and `amenities`. I standardize the remaining continuous features.

I split data into training data and test data. I fit regression models
with training data, predict outcomes on test data, and compare the
predicted outcomes to the actual outcomes.

I try 5 models: linear regression, lasso, KNN, random forest,
gradient-boosted trees.

I include all features and their interactions in linear regression.

Linear regression with too many features may result in overfitting.
Thus, I use lasso to regularize the above model. I use 10-fold cross
validation in the training data to find the optimal regularization
parameter *λ*.

I include all features in KNN. I use 10-fold cross validation in the
training data to find the optimal number of neighbors *k*.

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
<td style="text-align: left;">Linear regression</td>
<td style="text-align: right;">1063.74</td>
</tr>
<tr class="even">
<td style="text-align: left;">Lasso</td>
<td style="text-align: right;">1038.33</td>
</tr>
<tr class="odd">
<td style="text-align: left;">KNN</td>
<td style="text-align: right;">1013.65</td>
</tr>
<tr class="even">
<td style="text-align: left;">Random forest</td>
<td style="text-align: right;">807.75</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gradient-boosted trees</td>
<td style="text-align: right;">810.08</td>
</tr>
</tbody>
</table>

Random performs best with the lowest RMSE 807.75.

I am interested in the average change in revenue per square foot
associated with green certification, holding other features constant.
Thus, I plot partial dependence plots of 2 variables in the random
forest model (note the y-axis does not start from 0):  
![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%202-1.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%202-2.png)

From the graphs, green certification (either `LEED` = 1 or `EnergyStar`
= 1) increases the revenue per square foot.

## Predictive model building: California housing

I want to predict the median housing value in California. The outcome
variable is continuous, so it is a regression problem. I divide
`totalRooms` and `totalBedrooms` by `households` to get the number of
rooms/bedrooms per household. I standardize all features as they are
continuous.

I split data into training data and test data. I fit regression models
with training data, predict outcomes on test data, and compare the
predicted outcomes to the actual outcomes.

I try 5 models: linear regression, lasso, KNN, random forest,
gradient-boosted trees.

I include all features and their interactions in linear regression.

Linear regression with too many features may result in overfitting.
Thus, I use lasso to regularize the above model. I use 10-fold cross
validation in the training data to find the optimal regularization
parameter *λ*.

I include all features in KNN. I use 10-fold cross validation in the
training data to find the optimal number of neighbors *k*.

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
<td style="text-align: left;">Linear regression</td>
<td style="text-align: right;">66734.97</td>
</tr>
<tr class="even">
<td style="text-align: left;">Lasso</td>
<td style="text-align: right;">66476.58</td>
</tr>
<tr class="odd">
<td style="text-align: left;">KNN</td>
<td style="text-align: right;">60751.49</td>
</tr>
<tr class="even">
<td style="text-align: left;">Random forest</td>
<td style="text-align: right;">51213.69</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Gradient-boosted trees</td>
<td style="text-align: right;">44990.73</td>
</tr>
</tbody>
</table>

Gradient-boosted trees performs best with the lowest RMSE 45162.71.

Then I predict entire data (training + test) using gradient-boosted
trees. I plot `medianHouseValue`, predicted `medianHouseValue`, and
prediction errors on a California map.

Below is the plot for actual house value. Expensive houses (darker
points) are along the coast, from San Francisco to Los Angeles or San
Diego.  
![](Exercise-3-Answer_files/figure-markdown_strict/Map%20plots%20Real%20data-1.png)

Below is the plot for predicted house value. The pattern mostly aligns
with the actual data.  
![](Exercise-3-Answer_files/figure-markdown_strict/Map%20plots%20Prediction-1.png)

Below is the plot for prediction errors. Errors seem larger (darker
points) near Santa Barbara (34.5N, 120W).  
![](Exercise-3-Answer_files/figure-markdown_strict/Map%20plots%20Error-1.png)
