## Clustering and PCA

I want to use unsupervised learning to distinguish: 1. whether a wine is
red or white; 2. the quality of a wine. I first standardize 11 variables
(chemical properties).

Remember in unsupervised learning, there is no features (x) and outcomes
(y), no right or wrong, no accuracy.

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

I want to separate 7882 users into several market segments, based on the
categories of their Twitter posts. From the below data summary, most
third quantiles are 1, and most maximums are above 10, meaning variables
are highly right-skewed.

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
selecting the number of PCs, and you can try others if you want. I
standardize 36 variables here.

Then, I use K-means to cluster 3 projections of observations into 2
cluster. Again, there is no right or wrong for selecting the number of
clusters. In practice, people often select the number of clusters based
on their business problems.

I compare the average interests of all categories of two clusters. All
interests for cluster 1 are higher than those for cluster 2, meaning
they are more active users on Twitter.

    ## # A tibble: 2 × 37
    ##   cluster chatter current_events travel photo_sharing uncategorized tv_film
    ##     <dbl>   <dbl>          <dbl>  <dbl>         <dbl>         <dbl>   <dbl>
    ## 1       1    5.69           1.83   2.27          4.16          1.05    1.54
    ## 2       2    3.87           1.4    1.31          2.1           0.72    0.88
    ## # ℹ 30 more variables: sports_fandom <dbl>, politics <dbl>, food <dbl>,
    ## #   family <dbl>, home_and_garden <dbl>, music <dbl>, news <dbl>,
    ## #   online_gaming <dbl>, shopping <dbl>, health_nutrition <dbl>,
    ## #   college_uni <dbl>, sports_playing <dbl>, cooking <dbl>, eco <dbl>,
    ## #   computers <dbl>, business <dbl>, outdoors <dbl>, crafts <dbl>,
    ## #   automotive <dbl>, art <dbl>, religion <dbl>, beauty <dbl>, parenting <dbl>,
    ## #   dating <dbl>, school <dbl>, personal_fitness <dbl>, fashion <dbl>, …

Below is the number of users in each cluster:

    ## # A tibble: 2 × 2
    ## # Groups:   cluster [2]
    ##   cluster     n
    ##     <int> <int>
    ## 1       1  2282
    ## 2       2  5600

## Association rules for grocery purchases
