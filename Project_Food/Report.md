# Title

## Abstract

## Introduction

I started to record what I ate everyday in July 2022 by a very
incidental chance. Since then, I spent most of my time in Hong Kong
until I moved to Austin in July 2023. From my experience in HK, I was
wondering whether people tend to eat better (to relax or to compensate)
or simpler (to save time) when they are busy. However, my life and food
patterns in HK were so complicated and unpredictable to verify this
hypothesis. Considering the feasibility, I decide to estimate and
predict my life and food patterns in Austin.

It is worth noting that I have full discretion in the food recording
process, causing potential discrepancies and biases. For example, if I
have a brunch (at 10:00) and an afternoon tea (at 16:00), sometimes I
may record them as breakfast and lunch, but I may also record them as
lunch and dinner. Another discrepancy is the distinction between snacks
and meals. I may consider 50 g popcorn as snacks, then what about 51 g,
51.11 g, 50 g rice, etc.?

Beyond the discrepancies, I am not very confident in the predictive
accuracy for two additional reasons. First, the data set is small.
Second, although my life in Austin is simple due to some constraints,
the data is from a real human with certain flexibility and
unpredictability. However, it is still fun to know the driving factors
of my life and food patterns.

## Methods

### Data wrangling

The original data frame looks like this:

<table>
<colgroup>
<col style="width: 13%" />
<col style="width: 4%" />
<col style="width: 24%" />
<col style="width: 10%" />
<col style="width: 14%" />
<col style="width: 8%" />
<col style="width: 24%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">date</th>
<th style="text-align: left;">dow</th>
<th style="text-align: left;">breakfast</th>
<th style="text-align: left;">semester</th>
<th style="text-align: right;">week_of_sem</th>
<th style="text-align: left;">meal</th>
<th style="text-align: left;">food</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">2023-07-04</td>
<td style="text-align: left;">Tue</td>
<td style="text-align: left;">NA</td>
<td style="text-align: left;">summer</td>
<td style="text-align: right;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">SouthCloud Ramen</td>
</tr>
<tr class="even">
<td style="text-align: left;">2023-07-05</td>
<td style="text-align: left;">Wed</td>
<td style="text-align: left;">MA Econ orientation</td>
<td style="text-align: left;">summer</td>
<td style="text-align: right;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">MA Econ orientation</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2023-07-06</td>
<td style="text-align: left;">Thu</td>
<td style="text-align: left;">Home</td>
<td style="text-align: left;">summer</td>
<td style="text-align: right;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">Wendy’s</td>
</tr>
<tr class="even">
<td style="text-align: left;">2023-07-07</td>
<td style="text-align: left;">Fri</td>
<td style="text-align: left;">NA</td>
<td style="text-align: left;">summer</td>
<td style="text-align: right;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">Home</td>
</tr>
<tr class="odd">
<td style="text-align: left;">2023-07-07</td>
<td style="text-align: left;">Fri</td>
<td style="text-align: left;">NA</td>
<td style="text-align: left;">summer</td>
<td style="text-align: right;">0</td>
<td style="text-align: left;">dinner</td>
<td style="text-align: left;">China Family</td>
</tr>
<tr class="even">
<td style="text-align: left;">2023-07-08</td>
<td style="text-align: left;">Sat</td>
<td style="text-align: left;">NA</td>
<td style="text-align: left;">summer</td>
<td style="text-align: right;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">Home</td>
</tr>
</tbody>
</table>

I filter relevant `date` in Austin: after Jul 4, 2023 (inclusive),
exclude Thanksgiving holiday (from Nov 20 to Nov 26, both inclusive) and
winter vacation (from Dec 12, 2023 to Jan 11, 2024, both inclusive).

During this time, I am studying at The University of Texas at Austin, so
my life pattern heavily depends on the school calender. Thus, I create a
`semester` variable: it equals to “summer” when `date` is before Aug 14
(inclusive), equals to “fall” when `date` is after Aug 15 and before Dec
11 (both inclusive), and equals to “spring” otherwise.

Create `week_of_sem` column

## Check spring break

The variation in `breakfast` is close to zero as I eat at home most of
the time. To extract useful information, I convert `breakfast` to a
binary variable `breakfast_or_not`, because having breakfast may
indicate going out, and its food pattern may be different from staying
at home.

After all procedures, I delete unwanted columns. Below is the data frame
after processing:

<table>
<colgroup>
<col style="width: 4%" />
<col style="width: 11%" />
<col style="width: 14%" />
<col style="width: 8%" />
<col style="width: 13%" />
<col style="width: 20%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">dow</th>
<th style="text-align: left;">semester</th>
<th style="text-align: left;">week_of_sem</th>
<th style="text-align: left;">meal</th>
<th style="text-align: left;">food_class</th>
<th style="text-align: left;">breakfast_or_not</th>
<th style="text-align: right;">days_since_last_meal</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Wed</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">other</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">Thu</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">other</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Fri</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">dinner</td>
<td style="text-align: left;">other</td>
<td style="text-align: left;">0</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="even">
<td style="text-align: left;">Sat</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">home</td>
<td style="text-align: left;">0</td>
<td style="text-align: right;">1</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Sat</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">dinner</td>
<td style="text-align: left;">home</td>
<td style="text-align: left;">0</td>
<td style="text-align: right;">0</td>
</tr>
<tr class="even">
<td style="text-align: left;">Sun</td>
<td style="text-align: left;">summer</td>
<td style="text-align: left;">0</td>
<td style="text-align: left;">lunch</td>
<td style="text-align: left;">home</td>
<td style="text-align: left;">1</td>
<td style="text-align: right;">1</td>
</tr>
</tbody>
</table>

Number of meals in each category

    ## # A tibble: 3 × 2
    ## # Groups:   food_class [3]
    ##   food_class count
    ##   <fct>      <int>
    ## 1 canteen       86
    ## 2 home         204
    ## 3 other         63

## Results

## Conclusion
