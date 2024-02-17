## Saratoga house prices

I use two models to predict the house price in Saratoga: linear
regression and KNN regression. I use 10-fold cross validation and
out-of-sample RMSE to measure the model performance. I standardize
variables to improve model performance.

Below is the results of linear regression:

    ## Linear Regression 
    ## 
    ## 1728 samples
    ##   15 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (10 fold) 
    ## Summary of sample sizes: 1555, 1555, 1556, 1555, 1556, 1553, ... 
    ## Resampling results:
    ## 
    ##   RMSE       Rsquared   MAE      
    ##   0.5920207  0.6533476  0.4230834
    ## 
    ## Tuning parameter 'intercept' was held constant at a value of TRUE

Below is the results of KNN regression:

    ## k-Nearest Neighbors 
    ## 
    ## 1728 samples
    ##   15 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (10 fold) 
    ## Summary of sample sizes: 1555, 1556, 1555, 1555, 1554, 1556, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   k  RMSE       Rsquared   MAE      
    ##   5  0.6279333  0.6095152  0.4345010
    ##   7  0.6168284  0.6211978  0.4316882
    ##   9  0.6101807  0.6300309  0.4223517
    ## 
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final value used for the model was k = 9.

The linear regression model has better prediction performance, with a
lower RMSE.

## Classification and retrospective sampling

## Children and hotel reservations

### Model building

### Model validation: step 1

### Model validation: step 2

## Mushroom classification
