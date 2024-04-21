## Clustering and PCA

I want to use unsupervised learning to distinguish: 1. whether a wine is
red or white; 2.the quality of a wine. I first standardize 11 variables
(chemical properties).

Remember in unsupervised learning, there is no features and outcomes,
and there is no right or wrong, no accuracy.

### Clustering

To distinguish red wines from white wines, I use K-means to cluster data
into 2 clusters. Then I count the number of reds and whites in each
cluster. In the below table, each row is a cluster, and each column is
whether a wine is red or white. The algorithm can distinguish reds from
whites, as most whites are in cluster 1 and most reds are in cluster 2.

    ##    
    ##      red white
    ##   1 1581  2716
    ##   2   18  2182

As there are 7 levels of quality (3 - 9), I use K-means to cluster data
into 7 clusters. Then I count the quality in each cluster. In the below
table, each row is a cluster, and each column is the quality. The
algorithm cannot distinguish the quality, as the quality spreads out
among each cluster (row). There is no unique quality for each cluster.

    ##    
    ##       3   4   5   6   7   8   9
    ##   1   3  18 363 368 101  17   1
    ##   2   5  16 207 264 131  12   0
    ##   3   7  14 419 424  49  13   0
    ##   4   7  64 471 349  42   4   0
    ##   5   4  64 422 482 115  22   0
    ##   6   2  24 188 450 228  34   0
    ##   7   2  16  68 499 413  91   4

Alternatively, I cluster data into 2 clusters to try to distinguish
“high” vs. “low” quality. Similarly, the algorithm cannot distinguish
the quality.

    ##    
    ##        3    4    5    6    7    8    9
    ##   1   18  167 1257 1841  867  143    4
    ##   2   12   49  881  995  212   50    1

### PCA

I project 11 variables onto 3 principle components (PC). It is
acceptable to have more PCs, as the *n* + 1th PC will not affect all *n*
PCs. I calculate the projected values of observations on each PC.

I create a box plot of the projected values on PC1 for reds and whites.
The algorithm can distinguish reds from whites, as the projection for
reds are mostly lower than those for whites.
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
are similar across them. Results are similar on PC2 and PC3.
![](Exercise-4-Answer_files/figure-markdown_strict/pca%20quality%201-1.png)

Alternatively, I define the quality as “high” if it is greater than 5
and “low” otherwise. Then, I create a box plot of the projections on PC1
for high and low qualities. Similarly, the algorithm cannot distinguish
the quality.
![](Exercise-4-Answer_files/figure-markdown_strict/pca%20quality%202-1.png)

## Market segmentation

## Association rules for grocery purchases
