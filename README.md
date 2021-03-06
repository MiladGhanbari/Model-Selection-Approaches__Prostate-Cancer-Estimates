# Model Selection Approaches for Prostate Cancer Estimates
Several model selection strategies were implemented to find the best model fit to estimate prostate cancer. The prostate cancer data come from a study that examined the correlation between the level of prostate specific antigen and a number of clinical measures in men who were about to receive a radical prostatectomy. It is data frame with 97 rows and 9 columns. The data variables are as follows:

- lcavol: log(cancer volume)
- lweight: log(prostate weight)
- age: age of the patient
- lbph: log(benign prostatic hyperplasia amount)
- svi: seminal vesicle invasion
- lcp: log(capsular penetration)
- gleason: Gleason score
- pgg45: percentage Gleason scores 4 or 5
- lpsa: log(prostate specific antigen)

To combat overfitting, we usually look for the best model fit subject to a constraint on model complexity. So, we choose a model that has reasonable predictive power, but is not too complicated (i.e. not too many predictors). There are a large number of model selection methods, based on different criteria. We will examine the most common ones, namely, exhaustive search, forward selection, and backward selection. Furthermore, the focused criteria will be Akaike Information Criterion (AIC), Bayesian Information Criterion (BIC), and Adjusted R^2.


## Best subset strategy (exhaustive search)
The following graphs show the results of best subset strategy. A lower value of BIC corresponds to a better model fit. On the other hand, a higher value of R^2 adj corresponds to a better model fit. Therefore, based on BIC, the best model fit can be achieved using lcavol, lweight, and svi as model variables. Based on adjusted-R^2, the best model fit consists of all variables except gleason. The adjusted-R^2 is the simplest penalized model selection criterion and it tends to under-penalize the model complexity. The BIC penalizes model complexity more than adjusted-R^2 and is generally preferred over adjusted-R^2 for model selection purposes.

![alt text](ES_BIC.JPG)
![alt text](ES_AdjustedR2.JPG)


## Forward selection strategy
An alternative to the best subset strategy is forward selection. It has the following steps:
- Starts with no variables in the model
- Tests the addition of each variable using one of the selection criteria (AIC, BIC, etc.)
- Adds the new variable that improves the model the most
- Repeat until no remaining variables improve the model

The following is the summary of the selected best model by forward selection strategy using AIC criteria:

```sh
formula = lpsa ~ lcavol + lweight + svi + lbph + age

## Coefficients:
##                 Estimate 
## (Intercept)     0.49473 
## lcavol          0.54400 
## lweight         0.58821 
## svi             0.71490 
## lbph            0.10122 
## age            -0.01644 
```

## Backward selection strategy
Another alternative to the best subset strategy is backward selection:
- Start with all variables included in the model
- Test the deletion of each variable using one of the selection criteria (AIC, BIC, etc.)
- Delete the variable that results in the best model improvement once it has been removed
- Repeat this process until no further improvement is possible

The following is the summary of the selected best model by forward selection strategy using BIC criteria:

```sh
formula = lpsa ~ lcavol + lweight + svi

Coefficients:
##                Estimate 
## (Intercept)    -0.77716
## lcavol          0.52585
## lweight         0.66177
## svi             0.66567 
```
