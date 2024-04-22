## Clustering and PCA

I want to use unsupervised learning to distinguish: 1. whether a wine is
red or white; 2. the quality of a wine. I first standardize 11 variables
(chemical properties).

Remember in unsupervised learning, there is no features (x) and outcomes
(y), no prediction, no right or wrong, no accuracy.

### Clustering

To distinguish red wines from white wines, I use K-means to cluster data
into 2 clusters. Then I count the number of reds and whites in each
cluster. In the below table, each row is a cluster, and each column is
whether a wine is red or white. The algorithm can distinguish reds from
whites, as most whites are in cluster 1 and most reds are in cluster 2.

    ##    
    ##      red white
    ##   1   24  4830
    ##   2 1575    68

As there are 7 levels of quality (3 - 9), I use K-means to cluster data
into 7 clusters. Then I count the quality in each cluster. In the below
table, each row is a cluster, and each column is a quality level. The
algorithm cannot distinguish the quality, as the quality spreads out
among each cluster (row). There is no unique quality for each cluster.

    ##    
    ##       3   4   5   6   7   8   9
    ##   1   4  56 339 556 175  35   0
    ##   2   4  43 402 575 157  26   0
    ##   3   7  24 637 633 122  21   1
    ##   4   3  14  68 453 444  95   4
    ##   5   4  15 199 263 138  14   0
    ##   6   6  62 466 340  41   2   0
    ##   7   2   2  27  16   2   0   0

Alternatively, I cluster data into 2 clusters to try to distinguish
“high” vs. “low” quality. Similarly, the algorithm cannot distinguish
the quality.

    ##    
    ##        3    4    5    6    7    8    9
    ##   1   18  142 1436 2196  881  176    5
    ##   2   12   74  702  640  198   17    0

### PCA

I project 11 variables onto 3 principle components (PC). It is
acceptable to have more PCs, as the (*n*+1)-th PC will not affect all
*n* PCs. I calculate the projected values of all observations on each
PC.

I create a box plot of the projections on PC1 for reds and whites. The
algorithm can distinguish reds from whites, as the projection for reds
are mostly lower than those for whites.
![](Exercise-4-Answer_files/figure-markdown_strict/pca%20color%20plot-1.png)

More rigorously, I conduct a t-test to compare the mean projection of
reds and whites. Reds are significantly lower than whites.

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  pc1_red and pc1_white
    ## t = -125.74, df = 3053.8, p-value < 2.2e-16
    ## alternative hypothesis: true difference in means is not equal to 0
    ## 95 percent confidence interval:
    ##  -3.387295 -3.283278
    ## sample estimates:
    ##  mean of x  mean of y 
    ## -2.5144273  0.8208594

I create a box plot of the projections on PC1 for different qualities.
The algorithm cannot distinguish different qualities, as the projections
are similar across them. Results are similar for PC2 and PC3.
![](Exercise-4-Answer_files/figure-markdown_strict/pca%20quality%201-1.png)

Alternatively, I define the quality as “high” if it is greater than 5
and “low” otherwise. Then, I create a box plot of the projections on PC1
for high and low qualities. Similarly, the algorithm cannot distinguish
the quality.
![](Exercise-4-Answer_files/figure-markdown_strict/pca%20quality%202-1.png)

## Market segmentation

I want to separate 7882 users into several market segments, based on
interest categories of their Twitter posts. From the data summary below,
most third quantiles are 1 or 2, and most maximums are above 10, meaning
variables are highly right-skewed.

    ##     chatter       current_events      travel       photo_sharing   
    ##  Min.   : 0.000   Min.   :0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 2.000   1st Qu.:1.000   1st Qu.: 0.000   1st Qu.: 1.000  
    ##  Median : 3.000   Median :1.000   Median : 1.000   Median : 2.000  
    ##  Mean   : 4.399   Mean   :1.526   Mean   : 1.585   Mean   : 2.697  
    ##  3rd Qu.: 6.000   3rd Qu.:2.000   3rd Qu.: 2.000   3rd Qu.: 4.000  
    ##  Max.   :26.000   Max.   :8.000   Max.   :26.000   Max.   :21.000  
    ##  uncategorized      tv_film      sports_fandom       politics     
    ##  Min.   :0.000   Min.   : 0.00   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:0.000   1st Qu.: 0.00   1st Qu.: 0.000   1st Qu.: 0.000  
    ##  Median :1.000   Median : 1.00   Median : 1.000   Median : 1.000  
    ##  Mean   :0.813   Mean   : 1.07   Mean   : 1.594   Mean   : 1.789  
    ##  3rd Qu.:1.000   3rd Qu.: 1.00   3rd Qu.: 2.000   3rd Qu.: 2.000  
    ##  Max.   :9.000   Max.   :17.00   Max.   :20.000   Max.   :37.000  
    ##       food            family        home_and_garden      music        
    ##  Min.   : 0.000   Min.   : 0.0000   Min.   :0.0000   Min.   : 0.0000  
    ##  1st Qu.: 0.000   1st Qu.: 0.0000   1st Qu.:0.0000   1st Qu.: 0.0000  
    ##  Median : 1.000   Median : 1.0000   Median :0.0000   Median : 0.0000  
    ##  Mean   : 1.397   Mean   : 0.8639   Mean   :0.5207   Mean   : 0.6793  
    ##  3rd Qu.: 2.000   3rd Qu.: 1.0000   3rd Qu.:1.0000   3rd Qu.: 1.0000  
    ##  Max.   :16.000   Max.   :10.0000   Max.   :5.0000   Max.   :13.0000  
    ##       news        online_gaming       shopping      health_nutrition
    ##  Min.   : 0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.: 0.000   1st Qu.: 0.000   1st Qu.: 0.000   1st Qu.: 0.000  
    ##  Median : 0.000   Median : 0.000   Median : 1.000   Median : 1.000  
    ##  Mean   : 1.206   Mean   : 1.209   Mean   : 1.389   Mean   : 2.567  
    ##  3rd Qu.: 1.000   3rd Qu.: 1.000   3rd Qu.: 2.000   3rd Qu.: 3.000  
    ##  Max.   :20.000   Max.   :27.000   Max.   :12.000   Max.   :41.000  
    ##   college_uni     sports_playing      cooking            eco        
    ##  Min.   : 0.000   Min.   :0.0000   Min.   : 0.000   Min.   :0.0000  
    ##  1st Qu.: 0.000   1st Qu.:0.0000   1st Qu.: 0.000   1st Qu.:0.0000  
    ##  Median : 1.000   Median :0.0000   Median : 1.000   Median :0.0000  
    ##  Mean   : 1.549   Mean   :0.6392   Mean   : 1.998   Mean   :0.5123  
    ##  3rd Qu.: 2.000   3rd Qu.:1.0000   3rd Qu.: 2.000   3rd Qu.:1.0000  
    ##  Max.   :30.000   Max.   :8.0000   Max.   :33.000   Max.   :6.0000  
    ##    computers          business         outdoors           crafts      
    ##  Min.   : 0.0000   Min.   :0.0000   Min.   : 0.0000   Min.   :0.0000  
    ##  1st Qu.: 0.0000   1st Qu.:0.0000   1st Qu.: 0.0000   1st Qu.:0.0000  
    ##  Median : 0.0000   Median :0.0000   Median : 0.0000   Median :0.0000  
    ##  Mean   : 0.6491   Mean   :0.4232   Mean   : 0.7827   Mean   :0.5159  
    ##  3rd Qu.: 1.0000   3rd Qu.:1.0000   3rd Qu.: 1.0000   3rd Qu.:1.0000  
    ##  Max.   :16.0000   Max.   :6.0000   Max.   :12.0000   Max.   :7.0000  
    ##    automotive           art             religion          beauty       
    ##  Min.   : 0.0000   Min.   : 0.0000   Min.   : 0.000   Min.   : 0.0000  
    ##  1st Qu.: 0.0000   1st Qu.: 0.0000   1st Qu.: 0.000   1st Qu.: 0.0000  
    ##  Median : 0.0000   Median : 0.0000   Median : 0.000   Median : 0.0000  
    ##  Mean   : 0.8299   Mean   : 0.7248   Mean   : 1.095   Mean   : 0.7052  
    ##  3rd Qu.: 1.0000   3rd Qu.: 1.0000   3rd Qu.: 1.000   3rd Qu.: 1.0000  
    ##  Max.   :13.0000   Max.   :18.0000   Max.   :20.000   Max.   :14.0000  
    ##    parenting           dating            school        personal_fitness
    ##  Min.   : 0.0000   Min.   : 0.0000   Min.   : 0.0000   Min.   : 0.000  
    ##  1st Qu.: 0.0000   1st Qu.: 0.0000   1st Qu.: 0.0000   1st Qu.: 0.000  
    ##  Median : 0.0000   Median : 0.0000   Median : 0.0000   Median : 0.000  
    ##  Mean   : 0.9213   Mean   : 0.7109   Mean   : 0.7677   Mean   : 1.462  
    ##  3rd Qu.: 1.0000   3rd Qu.: 1.0000   3rd Qu.: 1.0000   3rd Qu.: 2.000  
    ##  Max.   :14.0000   Max.   :24.0000   Max.   :11.0000   Max.   :19.000  
    ##     fashion        small_business        spam             adult        
    ##  Min.   : 0.0000   Min.   :0.0000   Min.   :0.00000   Min.   : 0.0000  
    ##  1st Qu.: 0.0000   1st Qu.:0.0000   1st Qu.:0.00000   1st Qu.: 0.0000  
    ##  Median : 0.0000   Median :0.0000   Median :0.00000   Median : 0.0000  
    ##  Mean   : 0.9966   Mean   :0.3363   Mean   :0.00647   Mean   : 0.4033  
    ##  3rd Qu.: 1.0000   3rd Qu.:1.0000   3rd Qu.:0.00000   3rd Qu.: 0.0000  
    ##  Max.   :18.0000   Max.   :6.0000   Max.   :2.00000   Max.   :26.0000

Next, from the below correlation plot, there are 8 or 9
highly-correlated groups.  
![](Exercise-4-Answer_files/figure-markdown_strict/corr%20plot-1.png)

The information in 36 right-skewed categories is too sparse. Thus, I use
PCA to summarize them into 3 PCs. There is no right or wrong for
selecting the number of PCs, so you can try others if you want. I
standardize 36 variables here.

Then, I use K-means to cluster 3 projections of observations into 2
cluster. Again, there is no right or wrong for selecting the number of
clusters. In practice, people often select the number of clusters based
on their business problems.

I compare the average interests of all categories of two clusters. All
interests for cluster 1 are higher than those for cluster 2, meaning
users in cluster 1 are more active on Twitter. The company can focus on
cluster 1 to have more active response.

<table>
<colgroup>
<col style="width: 2%" />
<col style="width: 2%" />
<col style="width: 4%" />
<col style="width: 1%" />
<col style="width: 3%" />
<col style="width: 3%" />
<col style="width: 2%" />
<col style="width: 3%" />
<col style="width: 2%" />
<col style="width: 1%" />
<col style="width: 1%" />
<col style="width: 4%" />
<col style="width: 1%" />
<col style="width: 1%" />
<col style="width: 3%" />
<col style="width: 2%" />
<col style="width: 4%" />
<col style="width: 3%" />
<col style="width: 4%" />
<col style="width: 2%" />
<col style="width: 1%" />
<col style="width: 2%" />
<col style="width: 2%" />
<col style="width: 2%" />
<col style="width: 1%" />
<col style="width: 3%" />
<col style="width: 1%" />
<col style="width: 2%" />
<col style="width: 1%" />
<col style="width: 2%" />
<col style="width: 1%" />
<col style="width: 1%" />
<col style="width: 4%" />
<col style="width: 2%" />
<col style="width: 4%" />
<col style="width: 1%" />
<col style="width: 1%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: right;">cluster</th>
<th style="text-align: right;">chatter</th>
<th style="text-align: right;">current_events</th>
<th style="text-align: right;">travel</th>
<th style="text-align: right;">photo_sharing</th>
<th style="text-align: right;">uncategorized</th>
<th style="text-align: right;">tv_film</th>
<th style="text-align: right;">sports_fandom</th>
<th style="text-align: right;">politics</th>
<th style="text-align: right;">food</th>
<th style="text-align: right;">family</th>
<th style="text-align: right;">home_and_garden</th>
<th style="text-align: right;">music</th>
<th style="text-align: right;">news</th>
<th style="text-align: right;">online_gaming</th>
<th style="text-align: right;">shopping</th>
<th style="text-align: right;">health_nutrition</th>
<th style="text-align: right;">college_uni</th>
<th style="text-align: right;">sports_playing</th>
<th style="text-align: right;">cooking</th>
<th style="text-align: right;">eco</th>
<th style="text-align: right;">computers</th>
<th style="text-align: right;">business</th>
<th style="text-align: right;">outdoors</th>
<th style="text-align: right;">crafts</th>
<th style="text-align: right;">automotive</th>
<th style="text-align: right;">art</th>
<th style="text-align: right;">religion</th>
<th style="text-align: right;">beauty</th>
<th style="text-align: right;">parenting</th>
<th style="text-align: right;">dating</th>
<th style="text-align: right;">school</th>
<th style="text-align: right;">personal_fitness</th>
<th style="text-align: right;">fashion</th>
<th style="text-align: right;">small_business</th>
<th style="text-align: right;">spam</th>
<th style="text-align: right;">adult</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: right;">1</td>
<td style="text-align: right;">5.69</td>
<td style="text-align: right;">1.83</td>
<td style="text-align: right;">2.27</td>
<td style="text-align: right;">4.16</td>
<td style="text-align: right;">1.05</td>
<td style="text-align: right;">1.54</td>
<td style="text-align: right;">3.06</td>
<td style="text-align: right;">2.77</td>
<td style="text-align: right;">2.71</td>
<td style="text-align: right;">1.56</td>
<td style="text-align: right;">0.75</td>
<td style="text-align: right;">1.05</td>
<td style="text-align: right;">1.87</td>
<td style="text-align: right;">1.78</td>
<td style="text-align: right;">2.09</td>
<td style="text-align: right;">4.22</td>
<td style="text-align: right;">2.37</td>
<td style="text-align: right;">1.00</td>
<td style="text-align: right;">3.91</td>
<td style="text-align: right;">0.81</td>
<td style="text-align: right;">1.10</td>
<td style="text-align: right;">0.68</td>
<td style="text-align: right;">1.29</td>
<td style="text-align: right;">0.94</td>
<td style="text-align: right;">1.28</td>
<td style="text-align: right;">1.20</td>
<td style="text-align: right;">2.46</td>
<td style="text-align: right;">1.49</td>
<td style="text-align: right;">2.00</td>
<td style="text-align: right;">1.24</td>
<td style="text-align: right;">1.61</td>
<td style="text-align: right;">2.45</td>
<td style="text-align: right;">2.01</td>
<td style="text-align: right;">0.55</td>
<td style="text-align: right;">0.01</td>
<td style="text-align: right;">0.52</td>
</tr>
<tr class="even">
<td style="text-align: right;">2</td>
<td style="text-align: right;">3.87</td>
<td style="text-align: right;">1.40</td>
<td style="text-align: right;">1.31</td>
<td style="text-align: right;">2.10</td>
<td style="text-align: right;">0.72</td>
<td style="text-align: right;">0.88</td>
<td style="text-align: right;">0.99</td>
<td style="text-align: right;">1.39</td>
<td style="text-align: right;">0.86</td>
<td style="text-align: right;">0.58</td>
<td style="text-align: right;">0.43</td>
<td style="text-align: right;">0.53</td>
<td style="text-align: right;">0.94</td>
<td style="text-align: right;">0.98</td>
<td style="text-align: right;">1.10</td>
<td style="text-align: right;">1.89</td>
<td style="text-align: right;">1.21</td>
<td style="text-align: right;">0.49</td>
<td style="text-align: right;">1.22</td>
<td style="text-align: right;">0.39</td>
<td style="text-align: right;">0.47</td>
<td style="text-align: right;">0.32</td>
<td style="text-align: right;">0.57</td>
<td style="text-align: right;">0.34</td>
<td style="text-align: right;">0.65</td>
<td style="text-align: right;">0.53</td>
<td style="text-align: right;">0.54</td>
<td style="text-align: right;">0.39</td>
<td style="text-align: right;">0.48</td>
<td style="text-align: right;">0.50</td>
<td style="text-align: right;">0.43</td>
<td style="text-align: right;">1.06</td>
<td style="text-align: right;">0.58</td>
<td style="text-align: right;">0.25</td>
<td style="text-align: right;">0.01</td>
<td style="text-align: right;">0.36</td>
</tr>
</tbody>
</table>

Below is the number of users in each cluster:

<table>
<thead>
<tr class="header">
<th style="text-align: right;">cluster</th>
<th style="text-align: right;">count</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: right;">1</td>
<td style="text-align: right;">2282</td>
</tr>
<tr class="even">
<td style="text-align: right;">2</td>
<td style="text-align: right;">5600</td>
</tr>
</tbody>
</table>

## Association rules for grocery purchases

I want to find association rules for customers’ groceries shopping
basket. That means to find associated groceries that customers are
likely to buy, if they buy a grocery. I preprocess the data to fit into
`arules` package.

When finding association rules, I choose the minimum *support* as 0.005
and the minimum *confidence* as 0.25. So *lift* = *confidence* /
*support* = 50.  
- *Support* is the probability (proportion) of buying each grocery among
all purchases. I choose a relatively low threshold to include more
potential groceries.  
- *Confidence* is the conditional probability of buying a grocery, given
buying another grocery. I choose a relatively high threshold to focus on
major associations.  
- *Lift* measures the increased probability of buying a grocery, given
buying another grocery.  
For example, a toothbrush is purchased 5% of the time in general, and
40% of the time when customers purchase a toothpaste. Then the *support*
for toothbrush is 5%, the *confidence* is 40%, the *lift* is 8.

Below shows the distribution of *support*, *confidence*, and *lift* of
23 rules.  
![](Exercise-4-Answer_files/figure-markdown_strict/plot%20rules%20dist-1.png)

Below shows the network. *whole milk* and *other vegetables* are at the
center. Dairy products are associated with *whole milk*, and meats are
associated with *other vegetables*.  
![](Exercise-4-Answer_files/figure-markdown_strict/plot%20network-1.png)

## Image classification with neural networks

See Jupyter Notebook
