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

It measures the total variance in the response Y so the proportion of variability in Y that can be explained using X. $R^2$ is identical to the squared correlation. 


