# 3. Linear Regression

Can be used to answer the following questions: 

1. Is there a relationship between X and Y? 
2. How strong is the relationship between X and Y? 
3. What features are associated with Y? 
4. How large is the association between each feature and Y? 
5. How accurately can we predict Y? 
6. Is the relationship linear? 
7. Is there synergy between different features? 

## 3.1 Simple Linear Regression
$$Y \approx \beta_0 + \beta_1 X$$

**coefficients/ parameters:**
$\beta_0$ -> intercept; $\beta_1$ -> slope

### 3.1.1 Estimate the Coefficients 

> **residual sum of squares (RSS)**: 
> difference between the prediction and actual result squared
> 
> $$RSS = (y_1-\hat \beta_0 -\hat \beta_1x_1)^2 + ...+  (y_n-\hat \beta_0 -\hat \beta_1x_n)^2$$

### 3.1.2 Assessing the Accuracy of the Coefficient Estimates
> **population regression line:** optimal linear approximation of the relationship between X and Y (mostly unobtainable)

> **least squares line:** linear approximation with the least squares regression

<u>**estimating $\hat \mu$:**</u>

> unbiased estimations: the average of $\hat \mu $ over multiple training sets is equal to the actual $\mu$ (e.g. least squares coefficient)

> **standard error of $\hat \mu$:** 
> $$SE(\hat\mu)^2 = \frac{\sigma^2}{n}$$
> 
> higher n means lower standard error

> **residual standard error (RSE):** 
> $$RSE = \sqrt{\frac{RSS}{n-2}}$$
> 
> estimate of $\sigma$ 
> 
> can be used to compute confidence intervals

<u>**hypothesis tests on the coefficients**</u>

$H_0$: There is no relationship between X and Y. -> $\beta_1 = 0$

Test whether $\beta_1$ is sufficiently far away from 0 to be confident that $\beta_1$ is non-zero. This heavily depends on $SE(\hat\beta_1)$. 

If $SE(\hat\beta_1)$ is small, then small values of $\hat\beta_1$ might already provide evidence that the there is a relationship.

For this we calculate the number of standard deviations $\hat\beta_1$ is away from 0:
$$t = \frac{\hat\beta_1 - 0}{SE(\hat\beta_1)}$$

This formular is derived from this: 
$$t = \frac{Estimate - Hypothesized \space Value}{Standard \space Error}$$

The t-distribution shows how likely different t values are. It is centered on 0 and for $n>30$ it is very similar to normal distribution. Can be used to calculate p, that being the probability that T is bigger than $|t|$. If p is small then there is relationship between X and Y. 

> **p value:** If there were truly no relationship between 𝑋 and 𝑌 (i.e., 𝛽_1 = 0), how likely is it that we would observe a t-statistic at least this extreme by random chance?

### 3.1.3 Assessing the accuracy of the model
<u>**residual standard error:**</u>

Used to estimate of standard derivation of $\epsilon$. It is the average amount that the response will deviate from the true regression line. RSE is considered a measure of **lack of fit**. 

$$RSE = \sqrt{\frac{1}{n-2}RSS} = \sqrt{\frac{1}{n-2} \sum^n_{i=1}(y_i-\hat y_i)^2} $$

If RSE is small the fit is good.

<u>**$R^2$ Statistic**</u>

$R^2$ is independent of the scale of Y since it always has a value between 0 and 1. 

$$R^2 = 1- \frac{RSS}{TSS} = 1- \frac{\sum^n_{i=1}(y_i-\hat y_i)^2}{\sum^n_{i=1}(y_i-\overline y_i)^2}$$

TSS measures the total variance in the response Y, $R^2$ the proportion of variability in Y that can be explained using X. $R^2$ is identical to the squared correlation in the case of simple linear regression. In multiple linear regression it equals $Cor(Y, \hat Y)^2$.

$R^2$ will always increase if more predictors are added.

## 3.2 Multiple linear regression

$$Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + ... + \beta_p X_p + \epsilon$$

### 3.2.1 Estimating the regression coefficients

Parameters are still estimated using the least squares method. 

Does it make sense, that multiple regression suggest to relationship between $X_a$ and Y, while simple linear regression implies the opposite?
**Yes**: Consider a situation where $X_a$ and $X_b$ have a small correlation. If $X_a$ has a relationship with Y then the simple linear regression for both a and b suggest a relationship with Y because of their correlation. Multiple linear regression does not have this issue.

### 3.2.2 Some important questions
#### One: Is there a relationship between the response and the predictors?

$$H_0 = \forall i < p: \beta_i = 0$$

For this we use a F-statistic: 

$$F = \frac{\frac{1}{p}(TSS-RSS)}{\frac{1}{n-p-1} RSS}$$

Where:
$$TSS = \sum(y_i - \overline y)^2; \space \space RSS= \sum(y_i - \hat y)^2 $$ 

If the linear model assumptions are correct and $H_0$ ist true then $F = 1$. A larger F statistic is needed to reject $H_0$ if n is small. If $H_0$ is true and $\epsilon$ is normally distributed.

F-statistic adjusts for the number of predictors. 

#### Two: Deciding on important variables

Most of the time Y is only related to a subset of X. 

> Variable selection: determining which predictors are assciated with the response

The best way would be to check every combination of p for the best subset of p for the prediction. This would, however, mean that $2^p$ models need to be computed.
Other approaches: 

> Forward selection (Greedy): Begin with no predictors and add the predictor that results in the lowest RSS value... continue until it passes a certain threshold

> Backward selection: Begin with all predictors and always remove the predictor with the biggest p-value

> Mixed selection: Begin with no predictors and start with Backward selection. If the p-value of a predictor in the selected list gets to large, it will be removed.

#### Three: Model fit

$R^2$ and RSE are measures of model fit. If adding a new predictor improves $R^2$ significantly than the model with the new predicted is better than without it.  

Models with more variables can have higher RSE if the decrease in RSS is small relative to the increase in p. 

#### Four: Predictions

Three types of uncertainties are associated with the prediction: 

1. reducible error: estimate the true regression plane
2. bias: approximation of reality
3. random error

Therefore, we calculate confidence intervals to quantify the uncertainty in, for example, the average of a large number of datapoints. 
Prediction intervals are used to quantify the uncertainty in predictions for a specific datapoint. 

## 3.3 Other considerations in the regression model

### 3.3.1 Qualitative Predictors

**Dummy variables** (one-hot encoding) with to levels: code on to 1 and the other 0 or -1.

**Dummy variables** with multiple levels: 

$$
y_i = \beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \epsilon_i =
\begin{cases}
\beta_0 + \beta_1 + \epsilon_i & \text{if } i\text{th person is from the South} \\
\beta_0 + \beta_2 + \epsilon_i & \text{if } i\text{th person is from the West} \\
\beta_0 + \epsilon_i & \text{if } i\text{th person is from the East}
\end{cases}
$$

The level without a dummy variable is the baseline.

### 3.3.2 Extensions of the linear model 

Assumptions in linear models: 
1. relationship is linear
2. relationship is additive (association between $X_j$ and Y does not depend on the values of other predictors) (spending money on radio advertising might improve the effectivity of TV advertising)

#### Removing the Additive Assumption

Removing an **interaction effect**. It can be done with an interaction term: 

$$Y= \beta_0 + \beta_1X_1 + \beta_2X_2 + \beta_3X_1X_2 * \epsilon$$

> **hierarchical principal:** if an interaction term between a and b is in the model, then the **main effects** of a and b also need to be included

#### Non-linear Relationships

polynomial regression is still linear regression: 

$$Y = \beta_0 + \beta_1X_1 + \beta_2X_1^2 + \epsilon$$

Can also be done with, for example $\sqrt .$ or $log(.)$

### 3.3.3 Potential Problems

#### 1. Non-linearity of the Data

Use residual plots to identify non-linearity (see [residual plot](Chapter 3/some_additional_plots.ipynb)). 
If the residual plot shows a pattern, then there is a problem with the linear model.

#### 2. Correlation of error terms

The Assumption is that the error term of observation 1 is not correlated with that of observation 2. 
If this is not the case the SE is an underestimation. 
This frequently occurs in time series data. 

We can plot the residuals from our model as a function of time.
If there are noticeable patterns, then the assumption is likely not correct (adjacent residuals may have similar values).

Solution: good experiment design

#### 3. Non-constant Variance of error terms

> heteroscedasticity: non-constant variances in the errors

Can be identified if there is a funnel shape in the residual plot. 

Solution: use functions like $logY$ or $\sqrt Y$. OR weighted the least square ??

#### 4. Outliers

> **Outlier**: is a point for which $y_i$ is far from the predicted value.

Outliers with usual predictor values have little effect on the least squares fit.
It can, however, influence other parts of the linear regression (eg. the RSE).

Studentized residuals can be used to identify outliers. Residuals divided by the estimated standard error. 
Observations that have Studentized residual above 3 or below -3 are possible outliers. 

Solution: remove the outlier, or look for possible missing predictors that can explain the outliers

#### 5. High leverage points

> **High leverage points**: observations with unusual values for x

Have a bigger impact on the regression than outliers. 
Some observations might have normal values for each predictor, but the combination of those values might be unusual. 

A leverage statistic can be computed, to identify observations with high leverage. 

#### 6. Collinearity

> **Collinearity**: Two or more predictors are closely related to one another, they are correlated.

Can be identified using a variance inflation factor (VIF), which is the ratio of the variance of $\hat \beta_j$ when fitting the full model divided by the variance of $\hat \beta_j$ if fit on its own.

Solution: dropping problematic predictors or combining the two variables together

