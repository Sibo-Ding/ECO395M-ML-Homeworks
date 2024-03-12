# Estimate and Predict my Food Pattern in Austin Using Data Wrangling and Machine Learning

## Abstract

## Introduction

I started to record what I ate every day in July 2022 by a very
incidental chance. Since then, I spent most of my time in Hong Kong
until I moved to Austin in July 2023. From my experience in Hong Kong, I
was wondering whether people tend to eat better (to relax or to
compensate) or simpler (to save time) when they are busy. However, my
life and food patterns in Hong Kong were too complicated and
unpredictable to verify this hypothesis. Considering the feasibility, I
decide to estimate and predict my life and food patterns in Austin.

When recording meals, there are potential discrepancies and biases due
to my discretion. For example, if I have a brunch (at 10:00) and an
afternoon tea (at 16:00), sometimes I may record them as breakfast and
lunch, but I may also record them as lunch and dinner. Another
discrepancy is the vague distinction between snacks and meals. If I
consider 10 g popcorn as a snack, should I consider 11 g as a meal? If
so, then what about 10.1 g, 10.11 g, or 10 g rice, etc.?

Beyond the discrepancies, I am not very confident in the predictive
accuracy for two additional reasons. First, the data set is small.
Second, although my life in Austin is simple due to some constraints,
the data is from a real human with certain flexibility and
unpredictability. However, it is still fun to know the driving factors
of my life and food patterns.

## Methods

### Data wrangling

I keep `date` in Austin after Jul 4, 2023 (inclusive), exclude the
Thanksgiving holiday (from Nov 20 to Nov 26, both inclusive) and winter
vacation (from Dec 12, 2023 to Jan 11, 2024, both inclusive). The
initial data looks like this:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">date</th>
<th style="text-align: left;">dow</th>
<th style="text-align: left;">breakfast</th>
<th style="text-align: left;">lunch</th>
<th style="text-align: left;">dinner</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">7/4/2023</td>
<td style="text-align: left;">Tue</td>
<td style="text-align: left;">NA</td>
<td style="text-align: left;">SouthCloud Ramen</td>
<td style="text-align: left;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">7/5/2023</td>
<td style="text-align: left;">Wed</td>
<td style="text-align: left;">MA Econ orientation</td>
<td style="text-align: left;">MA Econ orientation</td>
<td style="text-align: left;">NA</td>
</tr>
<tr class="odd">
<td style="text-align: left;">7/6/2023</td>
<td style="text-align: left;">Thu</td>
<td style="text-align: left;">Home</td>
<td style="text-align: left;">Wendy’s</td>
<td style="text-align: left;">NA</td>
</tr>
<tr class="even">
<td style="text-align: left;">7/7/2023</td>
<td style="text-align: left;">Fri</td>
<td style="text-align: left;">NA</td>
<td style="text-align: left;">Home</td>
<td style="text-align: left;">China Family</td>
</tr>
<tr class="odd">
<td style="text-align: left;">7/8/2023</td>
<td style="text-align: left;">Sat</td>
<td style="text-align: left;">NA</td>
<td style="text-align: left;">Home</td>
<td style="text-align: left;">Home</td>
</tr>
<tr class="even">
<td style="text-align: left;">7/9/2023</td>
<td style="text-align: left;">Sun</td>
<td style="text-align: left;">Home</td>
<td style="text-align: left;">Home</td>
<td style="text-align: left;">NA</td>
</tr>
</tbody>
</table>

During this time, I am studying at The University of Texas at Austin, so
my life pattern heavily depends on the school calendar. Thus, I create a
`semester` variable: it is *summer* when `date` is before Aug 14
(inclusive), *fall* when `date` is after Aug 15 and before Dec 11 (both
inclusive), and *spring* otherwise.

For the same reason, I create a `week_of_sem` variable, where the first
week of a semester is 1, the second is 2, etc. Every week starts on
Monday or the first day of a semester if that day is not a Monday. I set
non-school days as 0, including spring break and days before or after
each semester.

The variation in `breakfast` is close to zero as I eat at home most of
the time. To extract useful information, I convert `breakfast` to a
binary variable `breakfast_or_not`, because having breakfast may
indicate going out, and its food pattern may be different from staying
at home.

I convert the data frame from wide format to long format.

I am interested in estimating and predicting my food pattern. For ease
of implementation, I create a `food_class` variable, where I classify
`food` into 3 categories: *home*, *canteen* (including *J2 Dining*,
*Jester City Limits*, and *Kins Dining*), and *other*.

Previous meals have impacts on the choice of the next meal. On one hand,
I may get bored with previous meals (diminishing marginal return). On
the other hand, I may be reluctant or constrained to change life and
food patterns. Therefore, I create a `days_since_last_meal` variable,
measuring the difference in `date` between a meal and the last meal with
the same `food_class`.

Here is the data after all processing:

<table>
<colgroup>
<col style="width: 13%" />
<col style="width: 8%" />
<col style="width: 11%" />
<col style="width: 14%" />
<col style="width: 4%" />
<col style="width: 20%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">food_class</th>
<th style="text-align: left;">meal</th>
<th style="text-align: left;">semester</th>
<th style="text-align: left;">week_of_sem</th>
<th style="text-align: left;">dow</th>
<th style="text-align: left;">breakfast_or_not</th>
<th style="text-align: right;">days_since_last_meal</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">other</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">Wed</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">other</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">Thu</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">other</td>
<td style="text-align: left;">dinner</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">Fri</td>
<td style="text-align: left;">0</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">home</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">Sat</td>
<td style="text-align: left;">0</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">home</td>
<td style="text-align: left;">dinner</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">Sat</td>
<td style="text-align: left;">0</td>
<td style="text-align: right;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">home</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">Sun</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">1</td>
</tr>
</tbody>
</table>

### Machine learning

The outcome variable (y variable) `food_class` is categorical. So this
can be a classification problem in supervised learning, or a clustering
problem in unsupervised learning. Features (x variables) are all
categorical except `days_since_last_meal` is continuous. Before any
analysis, let us look at the number of outcome variables in each
category:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">food_class</th>
<th style="text-align: right;">count</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">canteen</td>
<td style="text-align: right;">91</td>
</tr>
<tr class="even">
<td style="text-align: left;">home</td>
<td style="text-align: right;">211</td>
</tr>
<tr class="odd">
<td style="text-align: left;">other</td>
<td style="text-align: right;">65</td>
</tr>
</tbody>
</table>

I set 80% of the observations as training data, and 20% as test data.

#### Logistic regression

I include all features and their interactions in logistic regression.
The reason for including interactions is a lunch on Monday may be
different from a lunch on Saturday, depending on my class schedule.
Similar for interactions between `meal` and `semester`, etc.

#### Lasso

#### Random forest

I include all features in random forest.

#### Boosting

#### KNN

## Results

### Logistic regression

Below is the confusion matrix of logistic regression. Each column is an
original class, each row is a predicted class.

<table>
<thead>
<tr class="header">
<th style="text-align: left;"></th>
<th style="text-align: right;">canteen</th>
<th style="text-align: right;">home</th>
<th style="text-align: right;">other</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">canteen</td>
<td style="text-align: right;">11</td>
<td style="text-align: right;">3</td>
<td style="text-align: right;">2</td>
</tr>
<tr class="even">
<td style="text-align: left;">home</td>
<td style="text-align: right;">6</td>
<td style="text-align: right;">32</td>
<td style="text-align: right;">4</td>
</tr>
<tr class="odd">
<td style="text-align: left;">other</td>
<td style="text-align: right;">1</td>
<td style="text-align: right;">7</td>
<td style="text-align: right;">7</td>
</tr>
</tbody>
</table>

Overall accuracy measures the fraction of accurate predictions among all
observations. The overall accuracy is:

    ## [1] 0.6849315

Sensitivity measures the fraction of accurate predictions in each
original class (column). The sensitivities are:

    ## Class: canteen    Class: home   Class: other 
    ##      0.6111111      0.7619048      0.5384615

For example, in *canteen* column, there are **abba** accurate
predictions out of **bbaa**.

### Random forest

Confusion matrix:

<table>
<thead>
<tr class="header">
<th style="text-align: left;"></th>
<th style="text-align: right;">canteen</th>
<th style="text-align: right;">home</th>
<th style="text-align: right;">other</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">canteen</td>
<td style="text-align: right;">9</td>
<td style="text-align: right;">3</td>
<td style="text-align: right;">4</td>
</tr>
<tr class="even">
<td style="text-align: left;">home</td>
<td style="text-align: right;">9</td>
<td style="text-align: right;">37</td>
<td style="text-align: right;">2</td>
</tr>
<tr class="odd">
<td style="text-align: left;">other</td>
<td style="text-align: right;">0</td>
<td style="text-align: right;">2</td>
<td style="text-align: right;">7</td>
</tr>
</tbody>
</table>

Overall accuracy:

    ## [1] 0.7260274

Sensitivity:

    ## Class: canteen    Class: home   Class: other 
    ##      0.5000000      0.8809524      0.5384615

## Case study: driving factors of my food pattern

## Conclusion
