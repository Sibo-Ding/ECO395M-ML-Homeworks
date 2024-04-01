This file takes 6 minutes to knit. Chunks `Random forest 2` and
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
`total_cases` of dengue. The outcome variable is continuous, so it is a
regression problem. I convert `city` and `season` from strings to
categories. Below is the data after preprocessing:

<table>
<colgroup>
<col style="width: 1%" />
<col style="width: 2%" />
<col style="width: 3%" />
<col style="width: 5%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 7%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 7%" />
<col style="width: 6%" />
<col style="width: 6%" />
<col style="width: 9%" />
<col style="width: 11%" />
<col style="width: 7%" />
<col style="width: 3%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;"></th>
<th style="text-align: left;">city</th>
<th style="text-align: left;">season</th>
<th style="text-align: right;">total_cases</th>
<th style="text-align: right;">ndvi_ne</th>
<th style="text-align: right;">ndvi_nw</th>
<th style="text-align: right;">ndvi_se</th>
<th style="text-align: right;">ndvi_sw</th>
<th style="text-align: right;">precipitation_amt</th>
<th style="text-align: right;">air_temp_k</th>
<th style="text-align: right;">avg_temp_k</th>
<th style="text-align: right;">dew_point_temp_k</th>
<th style="text-align: right;">max_air_temp_k</th>
<th style="text-align: right;">min_air_temp_k</th>
<th style="text-align: right;">precip_amt_kg_per_m2</th>
<th style="text-align: right;">relative_humidity_percent</th>
<th style="text-align: right;">specific_humidity</th>
<th style="text-align: right;">tdtr_k</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">1</td>
<td style="text-align: left;">sj</td>
<td style="text-align: left;">spring</td>
<td style="text-align: right;">4</td>
<td style="text-align: right;">0.1226000</td>
<td style="text-align: right;">0.1037250</td>
<td style="text-align: right;">0.1984833</td>
<td style="text-align: right;">0.1776167</td>
<td style="text-align: right;">12.42</td>
<td style="text-align: right;">297.5729</td>
<td style="text-align: right;">297.7429</td>
<td style="text-align: right;">292.4143</td>
<td style="text-align: right;">299.8</td>
<td style="text-align: right;">295.9</td>
<td style="text-align: right;">32.00</td>
<td style="text-align: right;">73.36571</td>
<td style="text-align: right;">14.01286</td>
<td style="text-align: right;">2.628571</td>
</tr>
<tr class="even">
<td style="text-align: left;">2</td>
<td style="text-align: left;">sj</td>
<td style="text-align: left;">spring</td>
<td style="text-align: right;">5</td>
<td style="text-align: right;">0.1699000</td>
<td style="text-align: right;">0.1421750</td>
<td style="text-align: right;">0.1623571</td>
<td style="text-align: right;">0.1554857</td>
<td style="text-align: right;">22.82</td>
<td style="text-align: right;">298.2114</td>
<td style="text-align: right;">298.4429</td>
<td style="text-align: right;">293.9514</td>
<td style="text-align: right;">300.9</td>
<td style="text-align: right;">296.4</td>
<td style="text-align: right;">17.94</td>
<td style="text-align: right;">77.36857</td>
<td style="text-align: right;">15.37286</td>
<td style="text-align: right;">2.371429</td>
</tr>
<tr class="odd">
<td style="text-align: left;">3</td>
<td style="text-align: left;">sj</td>
<td style="text-align: left;">spring</td>
<td style="text-align: right;">4</td>
<td style="text-align: right;">0.0322500</td>
<td style="text-align: right;">0.1729667</td>
<td style="text-align: right;">0.1572000</td>
<td style="text-align: right;">0.1708429</td>
<td style="text-align: right;">34.54</td>
<td style="text-align: right;">298.7814</td>
<td style="text-align: right;">298.8786</td>
<td style="text-align: right;">295.4343</td>
<td style="text-align: right;">300.5</td>
<td style="text-align: right;">297.3</td>
<td style="text-align: right;">26.10</td>
<td style="text-align: right;">82.05286</td>
<td style="text-align: right;">16.84857</td>
<td style="text-align: right;">2.300000</td>
</tr>
<tr class="even">
<td style="text-align: left;">4</td>
<td style="text-align: left;">sj</td>
<td style="text-align: left;">spring</td>
<td style="text-align: right;">3</td>
<td style="text-align: right;">0.1286333</td>
<td style="text-align: right;">0.2450667</td>
<td style="text-align: right;">0.2275571</td>
<td style="text-align: right;">0.2358857</td>
<td style="text-align: right;">15.36</td>
<td style="text-align: right;">298.9871</td>
<td style="text-align: right;">299.2286</td>
<td style="text-align: right;">295.3100</td>
<td style="text-align: right;">301.4</td>
<td style="text-align: right;">297.0</td>
<td style="text-align: right;">13.90</td>
<td style="text-align: right;">80.33714</td>
<td style="text-align: right;">16.67286</td>
<td style="text-align: right;">2.428571</td>
</tr>
<tr class="odd">
<td style="text-align: left;">5</td>
<td style="text-align: left;">sj</td>
<td style="text-align: left;">spring</td>
<td style="text-align: right;">6</td>
<td style="text-align: right;">0.1962000</td>
<td style="text-align: right;">0.2622000</td>
<td style="text-align: right;">0.2512000</td>
<td style="text-align: right;">0.2473400</td>
<td style="text-align: right;">7.52</td>
<td style="text-align: right;">299.5186</td>
<td style="text-align: right;">299.6643</td>
<td style="text-align: right;">295.8214</td>
<td style="text-align: right;">301.9</td>
<td style="text-align: right;">297.5</td>
<td style="text-align: right;">12.20</td>
<td style="text-align: right;">80.46000</td>
<td style="text-align: right;">17.21000</td>
<td style="text-align: right;">3.014286</td>
</tr>
<tr class="even">
<td style="text-align: left;">7</td>
<td style="text-align: left;">sj</td>
<td style="text-align: left;">summer</td>
<td style="text-align: right;">4</td>
<td style="text-align: right;">0.1129000</td>
<td style="text-align: right;">0.0928000</td>
<td style="text-align: right;">0.2050714</td>
<td style="text-align: right;">0.2102714</td>
<td style="text-align: right;">3.48</td>
<td style="text-align: right;">299.2071</td>
<td style="text-align: right;">299.2214</td>
<td style="text-align: right;">295.8657</td>
<td style="text-align: right;">301.3</td>
<td style="text-align: right;">297.7</td>
<td style="text-align: right;">38.60</td>
<td style="text-align: right;">82.00000</td>
<td style="text-align: right;">17.23429</td>
<td style="text-align: right;">2.042857</td>
</tr>
</tbody>
</table>

I split data into training data and test data. I fit regression models
with training data, predict outcomes on test data, and compare the
predicted outcomes to the actual outcomes.

I include all features in CART. I use 10-fold cross validation in the
training data to find the optimal complexity parameter.

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

Partial dependence plots for 3 variables in the random forest model:
![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%201-1.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%201-2.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%201-3.png)

From the plots, dengue is more prevalent on more humid days and in fall.

## Predictive model building: green certification

I want to predict rental revenue per square foot per calendar year for
commercial properties in the US. The outcome variable is continuous, so
it is a regression problem. I calculate revenue per foot year as the
product of `Rent` and `leasing_rate`. After that, I drop `Rent`,
`leasing_rate` and two identifiers. I convert 8 features from continuous
to categorical, which are `renovated`, `class_a`, `class_b`, `LEED`,
`Energystar`, `green_rating`, `net`, and `amenities`. I standardize the
remaining continuous features. Below is the data after preprocessing:

<table>
<colgroup>
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 4%" />
<col style="width: 3%" />
<col style="width: 3%" />
<col style="width: 2%" />
<col style="width: 4%" />
<col style="width: 5%" />
<col style="width: 1%" />
<col style="width: 4%" />
<col style="width: 5%" />
<col style="width: 4%" />
<col style="width: 5%" />
<col style="width: 6%" />
<col style="width: 4%" />
<col style="width: 8%" />
<col style="width: 7%" />
<col style="width: 7%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: right;">size</th>
<th style="text-align: right;">empl_gr</th>
<th style="text-align: right;">stories</th>
<th style="text-align: right;">age</th>
<th style="text-align: left;">renovated</th>
<th style="text-align: left;">class_a</th>
<th style="text-align: left;">class_b</th>
<th style="text-align: left;">LEED</th>
<th style="text-align: left;">Energystar</th>
<th style="text-align: left;">green_rating</th>
<th style="text-align: left;">net</th>
<th style="text-align: left;">amenities</th>
<th style="text-align: right;">cd_total_07</th>
<th style="text-align: right;">hd_total07</th>
<th style="text-align: right;">total_dd_07</th>
<th style="text-align: right;">Precipitation</th>
<th style="text-align: right;">Gas_Costs</th>
<th style="text-align: right;">Electricity_Costs</th>
<th style="text-align: right;">City_Market_Rent</th>
<th style="text-align: right;">revenue_per_sqft</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: right;">0.0854131</td>
<td style="text-align: right;">-0.1208773</td>
<td style="text-align: right;">0.0332689</td>
<td style="text-align: right;">-0.9706496</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">3.385385</td>
<td style="text-align: right;">-1.698857</td>
<td style="text-align: right;">0.2034667</td>
<td style="text-align: right;">1.031788</td>
<td style="text-align: right;">1.000556</td>
<td style="text-align: right;">-0.2167905</td>
<td style="text-align: right;">0.8732548</td>
<td style="text-align: right;">3523.998</td>
</tr>
<tr class="even">
<td style="text-align: right;">-0.5600798</td>
<td style="text-align: right;">-0.1208773</td>
<td style="text-align: right;">-0.6975245</td>
<td style="text-align: right;">-0.6273486</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">3.385385</td>
<td style="text-align: right;">-1.698857</td>
<td style="text-align: right;">0.2034667</td>
<td style="text-align: right;">1.031788</td>
<td style="text-align: right;">1.013709</td>
<td style="text-align: right;">-0.2115382</td>
<td style="text-align: right;">0.8732548</td>
<td style="text-align: right;">2489.590</td>
</tr>
<tr class="odd">
<td style="text-align: right;">-0.2347590</td>
<td style="text-align: right;">-0.1208773</td>
<td style="text-align: right;">-0.0479304</td>
<td style="text-align: right;">-0.3464659</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">3.385385</td>
<td style="text-align: right;">-1.698857</td>
<td style="text-align: right;">0.2034667</td>
<td style="text-align: right;">1.031788</td>
<td style="text-align: right;">1.013709</td>
<td style="text-align: right;">-0.2115382</td>
<td style="text-align: right;">0.8732548</td>
<td style="text-align: right;">2962.591</td>
</tr>
<tr class="even">
<td style="text-align: right;">-0.4745090</td>
<td style="text-align: right;">-0.1208773</td>
<td style="text-align: right;">-0.0479304</td>
<td style="text-align: right;">-0.0343740</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: right;">3.385385</td>
<td style="text-align: right;">-1.698857</td>
<td style="text-align: right;">0.2034667</td>
<td style="text-align: right;">1.031788</td>
<td style="text-align: right;">1.013709</td>
<td style="text-align: right;">-0.2115382</td>
<td style="text-align: right;">0.8732548</td>
<td style="text-align: right;">3396.400</td>
</tr>
<tr class="odd">
<td style="text-align: right;">-0.2030309</td>
<td style="text-align: right;">-0.1208773</td>
<td style="text-align: right;">0.1956674</td>
<td style="text-align: right;">-1.3139507</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">3.385385</td>
<td style="text-align: right;">-1.698857</td>
<td style="text-align: right;">0.2034667</td>
<td style="text-align: right;">1.031788</td>
<td style="text-align: right;">1.013709</td>
<td style="text-align: right;">-0.2115382</td>
<td style="text-align: right;">0.8732548</td>
<td style="text-align: right;">3929.840</td>
</tr>
<tr class="even">
<td style="text-align: right;">-0.0107438</td>
<td style="text-align: right;">-0.1208773</td>
<td style="text-align: right;">0.0332689</td>
<td style="text-align: right;">-0.8458129</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">3.385385</td>
<td style="text-align: right;">-1.698857</td>
<td style="text-align: right;">0.2034667</td>
<td style="text-align: right;">1.031788</td>
<td style="text-align: right;">1.013709</td>
<td style="text-align: right;">-0.2115382</td>
<td style="text-align: right;">0.8732548</td>
<td style="text-align: right;">4002.658</td>
</tr>
</tbody>
</table>

I split data into training data and test data. I fit regression models
with training data, predict outcomes on test data, and compare the
predicted outcomes to the actual outcomes.

I try 5 models: linear regression, lasso, KNN, random forest, and GBM.

I include all features and their interactions in linear regression.

Linear regression with too many features may result in overfitting.
Thus, I use lasso to regularize the above model. I use 10-fold cross
validation in the training data to find the optimal regularization
parameter *λ*.

I include all features in KNN. I use 10-fold cross validation in the
training data to find the optimal number of neighbors *k*.

I include all features in random forest.

I include all features in GBM. I manually tune several parameters.

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
<td style="text-align: left;">GBM</td>
<td style="text-align: right;">810.08</td>
</tr>
</tbody>
</table>

Random performs best with the lowest RMSE 807.75.

I am interested in the average change in revenue per square foot
associated with green certification, holding other features constant.
Thus, I plot partial dependence plots for 2 variables in the random
forest model (note the y-axis does not start from 0):  
![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%202-1.png)![](Exercise-3-Answer_files/figure-markdown_strict/Partial%20dependence%20plots%202-2.png)

From the plots, green certification (either `LEED` = 1 or `EnergyStar`
= 1) increases the revenue per square foot.

## Predictive model building: California housing

I want to predict the median housing value in California. The outcome
variable is continuous, so it is a regression problem. I divide
`totalRooms` and `totalBedrooms` by `households` to get the number of
rooms/bedrooms per household. I standardize all features as they are
continuous. Below is the data after preprocessing:

<table style="width:100%;">
<colgroup>
<col style="width: 9%" />
<col style="width: 8%" />
<col style="width: 15%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 11%" />
<col style="width: 15%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: right;">longitude</th>
<th style="text-align: right;">latitude</th>
<th style="text-align: right;">housingMedianAge</th>
<th style="text-align: right;">rooms</th>
<th style="text-align: right;">bedrooms</th>
<th style="text-align: right;">population</th>
<th style="text-align: right;">households</th>
<th style="text-align: right;">medianIncome</th>
<th style="text-align: right;">medianHouseValue</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: right;">-1.327803</td>
<td style="text-align: right;">1.052523</td>
<td style="text-align: right;">0.9821189</td>
<td style="text-align: right;">0.6285442</td>
<td style="text-align: right;">-0.1537539</td>
<td style="text-align: right;">-0.9744050</td>
<td style="text-align: right;">-0.9770092</td>
<td style="text-align: right;">2.3447090</td>
<td style="text-align: right;">452600</td>
</tr>
<tr class="even">
<td style="text-align: right;">-1.322812</td>
<td style="text-align: right;">1.043159</td>
<td style="text-align: right;">-0.6070042</td>
<td style="text-align: right;">0.3270334</td>
<td style="text-align: right;">-0.2633294</td>
<td style="text-align: right;">0.8614180</td>
<td style="text-align: right;">1.6699206</td>
<td style="text-align: right;">2.3321815</td>
<td style="text-align: right;">358500</td>
</tr>
<tr class="odd">
<td style="text-align: right;">-1.332794</td>
<td style="text-align: right;">1.038477</td>
<td style="text-align: right;">1.8561366</td>
<td style="text-align: right;">1.1555925</td>
<td style="text-align: right;">-0.0490152</td>
<td style="text-align: right;">-0.8207575</td>
<td style="text-align: right;">-0.8436165</td>
<td style="text-align: right;">1.7826562</td>
<td style="text-align: right;">352100</td>
</tr>
<tr class="even">
<td style="text-align: right;">-1.337785</td>
<td style="text-align: right;">1.038477</td>
<td style="text-align: right;">1.8561366</td>
<td style="text-align: right;">0.1569623</td>
<td style="text-align: right;">-0.0498317</td>
<td style="text-align: right;">-0.7660095</td>
<td style="text-align: right;">-0.7337637</td>
<td style="text-align: right;">0.9329449</td>
<td style="text-align: right;">341300</td>
</tr>
<tr class="odd">
<td style="text-align: right;">-1.337785</td>
<td style="text-align: right;">1.038477</td>
<td style="text-align: right;">1.8561366</td>
<td style="text-align: right;">0.3447024</td>
<td style="text-align: right;">-0.0329051</td>
<td style="text-align: right;">-0.7598283</td>
<td style="text-align: right;">-0.6291419</td>
<td style="text-align: right;">-0.0128807</td>
<td style="text-align: right;">342200</td>
</tr>
<tr class="even">
<td style="text-align: right;">-1.337785</td>
<td style="text-align: right;">1.038477</td>
<td style="text-align: right;">1.8561366</td>
<td style="text-align: right;">-0.2697231</td>
<td style="text-align: right;">0.0146690</td>
<td style="text-align: right;">-0.8940491</td>
<td style="text-align: right;">-0.8017678</td>
<td style="text-align: right;">0.0874445</td>
<td style="text-align: right;">269700</td>
</tr>
</tbody>
</table>

I split data into training data and test data. I fit regression models
with training data, predict outcomes on test data, and compare the
predicted outcomes to the actual outcomes.

I try 5 models: linear regression, lasso, KNN, random forest, and GBM.

I include all features and their interactions in linear regression.

Linear regression with too many features may result in overfitting.
Thus, I use lasso to regularize the above model. I use 10-fold cross
validation in the training data to find the optimal regularization
parameter *λ*.

I include all features in KNN. I use 10-fold cross validation in the
training data to find the optimal number of neighbors *k*.

I include all features in random forest.

I include all features in GBM. I manually tune several parameters.

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
<td style="text-align: left;">GBM</td>
<td style="text-align: right;">44990.73</td>
</tr>
</tbody>
</table>

GBM performs best with the lowest RMSE 44990.73.

Then I predict entire data (training + test) using GBM. I plot
`medianHouseValue`, predicted `medianHouseValue`, and prediction errors
on a California map.

Below is the plot for actual house value. Expensive houses (darker
points) are along the coast, from San Francisco to Los Angeles / San
Diego.  
![](Exercise-3-Answer_files/figure-markdown_strict/Map%20plot%20Real%20data-1.png)

Below is the plot for predicted house value. The pattern mostly aligns
with the actual data.  
![](Exercise-3-Answer_files/figure-markdown_strict/Map%20plot%20Prediction-1.png)

Below is the plot for prediction errors. Errors seem larger (darker
points) near Santa Barbara (34.5N, 120W).  
![](Exercise-3-Answer_files/figure-markdown_strict/Map%20plot%20Error-1.png)
