# ATE and ATT

Suppose $Y$ is an outcome random variable, $A$ is a indicator variable to represent the presence of treatment, for example $A={0,1}$ in binary treatment case. For example, $A=1$ is a condition to represent the diabetes patient population administered the insulin, while $A=0$ is for not administered.

Also, suppose $Y_{a}$ is an outcome when the treatment is SET to $a$; for example, $Y_{a=1}$ is an outcome random variable when the treatment class is $1$ regardless of the actual treatment applied in observing $Y$. This means the random variable $Y_{a=1} | A=0$ can exist and this represents the 'what-if' random variable $Y$ in a sense that it is the random variable under the condition of not being treated ( $A=0$ ) but what if it was treated ( $a=0$ ).

For example, $Y_{a=1} | A=0$ can give the random variable of *HbA1C* for the patient group who was not administered the insulin but in the case if they had been administered. 

Here the $ATE$ (Average Treatment Effect) and $ATT$ (Average Treatment Effect of the Treated) are introduced.

## *ATE* (Average Treatment Effect)

$ATE = \mathbb{E}[Y_{a=1}-Y_{a=0}]$

This represents the expectation of the effect of the treatment in a sense it takes the difference of the outcome random variables, the former is if whole population was set in the treated group while the latter is if set in the non-treated group.

## *ATT* (Average Treatment Effect of the Treated)

$ATT = \mathbb{E}[Y_{a=1}-Y_{a=0}|A=1]$

This represents the similar expectatino of effect to *ATE* with the only difference in the random variable in interest are only from the population who was actually treated because it is conditioned by $A=1$.

## *ATE* vs. *ATT* in an example

Let's describe the difference of *ATE* and *ATT* in English with an example of insulin patient. 

*ATE* is the expected effect of insulin against the entire population in interest.

*ATT* is the expected effect of insulin against the population who was actually given insulin, and disregarding the population who was not given insulin--supposedly they are severer diabetic patients because the physicians found out they should take the insulin.

$<br \ >$



