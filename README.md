# Concept of Counterfactual
XXXXXXXXXXXXXXXXXXXX [TO BE ENRICHED LATER] 

$<br \ ><br \ >$

# Approaches to Reach Couterfactual in Special Circumstances
- DID
- RDD
- Instrumental Variable (IV) Estimation

XXXXXXXXXXXXXXXXXXXX [TO BE ENRICHED LATER] 

$<br \ ><br \ >$

# ATE (Average Treatment Effect) and ATT (Average Treatment Effect of the Treated)

Suppose $Y$ is an outcome random variable, $A$ is a indicator variable to represent the presence of treatment, for example $A \in \lbrace 0,1 \rbrace$ in binary treatment case. For example, $A=1$ is a condition to represent the diabetes patient population is administered the insulin, while $A=0$ is for not administered.

Also, suppose $Y_{a}$ is an outcome when the treatment is SET to $a$; for example, $Y_{a=1}$ is an outcome random variable when the treatment class is $1$ regardless of the actual treatment applied in observing $Y$. This means the random variable $Y_{a=1} | A=0$ can exist and this represents the 'what-if' value of $Y$ in a sense that it is the random variable under the condition of not being treated ( $A=0$ ) but what if it was treated ( $a=1$ ).

For example, $Y_{a=1} | A=0$ can give the random variable of *HbA1C* for the patient group who was not administered the insulin but in the virtual case if they had been administered. 

Here the $ATE$ (Average Treatment Effect) and $ATT$ (Average Treatment Effect of the Treated) are introduced.

$<br \ >$

## *ATE* (Average Treatment Effect)

$ATE \ = \ \mathbb{E}[Y_{a=1}-Y_{a=0}]$

This represents the expectation of the effect of the treatment in a sense it takes the difference of the outcome random variables, the former is if whole population was set in the treated group while the latter is if set in the non-treated group.

$<br \ >$

## *ATT* (Average Treatment Effect of the Treated)

$ATT \ = \ \mathbb{E}[Y_{a=1}-Y_{a=0}|A=1]$

This represents the similar expectatino of effect to *ATE* with the only difference in the random variable in interest are only from the population who was actually treated because it is conditioned by $A=1$.

$<br \ >$

## *ATE* vs. *ATT* in an example

Let's describe the difference of *ATE* and *ATT* in English with an example of insulin patient. 

- *ATE* is the expected effect of insulin (e.g. decrease in *HbA1C*) against the entire population in interest.

- *ATT* is the expected effect of insulin against the population who was actually given insulin, and disregarding the population who was not given insulin--supposedly they are severer diabetic patients because the physicians found out they should take the insulin.

$<br \ ><br \ >$

# Rondomized control trial

If the treatment assignment is randomly controlled, the assignment of $A$ is random, *ATE* is equivalent to

$\mathbb{E}[Y|(A=1) \ - \ Y|(A=0)] \ = \ \mathbb{E}[Y|(A=1)] \ - \ \mathbb{E}[Y|(A=0)]$.

In the insulin example, this happens when the patients given insulin are the ones selected randomly with no influence from any attributional factors such as the disease severity, age, or etc. In this situation, we can get the unbiased estimate of effect of insulin by just taking the average of difference of *HbA1C* in the population assigned to treatment group and that in the population assigned to non-treatment group.

$<br \ >$

Here's the proof of this property:

------------------

When $A$ is assigned randomly, $Y_{a} \perp A$ for $a \ \in \ \{0,1\}$. This leads to:

$Y_{a=1} \ = \ Y_{a=1}|(A=1) \ = \ Y_{a=1}|(A=0)$ and $Y_{a=0} \ = \ Y_{a=0}|(A=0) \ = \ Y_{a=0}|(A=1)$, (also known as *exchangeability*).

Here, under the RCT set up, we can say the assignment of treatment/non-treatment group $A=a'$ is equivalized to the use of set notation $Y_{a=a'}$ (in RCT, two groups of sujects are 'forced' to comply the individual assignment).

This should result in:

$Y_{a} \ = \ Y$ for $a=$ 0 or 1. (also known as *consistency*)

$<br \ >$

Therefore,

$$
\begin{aligned}
ATE \ & = \ \mathbb{E}[Y_{a=1} \ - \ Y_{a=0}] \\
& = \ \mathbb{E}[Y_{a=1}] \ - \ \mathbb{E}[Y_{a=0}] \\
& = \ \mathbb{E}[Y_{a=1}|A=1] \ - \ \mathbb{E}[Y_{a=0}|A=0] \\
& = \ \mathbb{E}[Y|A=1] \ - \ \mathbb{E}[Y|A=0] \\
& = \ treatment \ effect \ calculated \ under \ RCT
\end{aligned}
$$


Where the second line to the third uses *exchangeability* and the third to the fourth uses *consistency*.

Now, it proves the $ATE \ = \ treatment \ effect \ calculated \ under \ RCT$

------------------

$<br \ >$

This indicates that under the RCT set up, it is possible to say that the difference in plain averages of each group (treatment/non-treatment (control)) directly becomes the unbiased estimate of the ATE.

$<br \ >$

Although it is true that RCT solves the issue in the estimate of treatment effect, it is not always possible to do RCT in real life for various reasons in costs, ethics, and etc. Also, let's take the fact into account that there is already a lot of data collected through non-RCT context ready for being utilized without further data collection efforts. That is why the studies in how to get the value of treatment effect through observational data are appreciated.

$<br \ ><br \ >$

# Population Bias

The challenge appears though when using observational data. Primarily, the lack of $Y_{a} \perp A$ or *exchangeability* is an issue. In plain English, this means the outcome for the treated group and the outcome for the untreated group are not equivalent. For examples:
- the effect of insulin is not the same to the patients who are administered and the ones who are not; because it depends on the doctors' discretions and the former patient group is supposedly under severer condition than the latter.
- the effect of marketing campaign such as coupon distribution is not the same to the customers who received the coupon and the ones who do not; because it depends on the marketing team's discretion and the former customer group is supposedly promising and sensitive to the campaign than the latter.

In general, this limitation is just called **population bias**. Next section shows one of the possible approaches we can take to tackle this limitation and get the unbiased estimate of the treatment effect.

$<br \ ><br \ >$

# Inverse Probability Weighting

When we can get the probabilities of the assignment, i.e. $P[A=1]$ and $P[A=0]$, it is possible to get the unbiased estimate of *ATE* and *ATT* from the observational data. This method is called Inversed Probability Weighting.

Under the observational data, we have a set of observational data, $\lbrace ( Y_{i}, A_{i} ) \rbrace^{n}_{i=1}$. The Inversed Probability Weighted Estimator (*IPWE*) for $a=a'$ is given by:

$\hat{\mu}^{IPWE}\_{a'} \ = \ \frac{1}{n} \sum\limits_{i=1}^{n} Y_{i} \frac{1_{A_i=a'}}{P[A_i=a']}$

This *IPWE* is an unbiased estimator of $Y_{a=a'}$, namely $\mathbb{E}[\hat{\mu}^{IPWE}\_{a'}] \ = \ Y_{a=a'}$.

$<br \ >$

Here's the proof of this property:

---

---

$<br \ ><br \ >$

# Reference

- "Causal Inference: What If", Miguel A. Hernan, James M. Robins, CRC Press, https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/

