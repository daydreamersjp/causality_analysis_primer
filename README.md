# Concept of Counterfactual
XXXXXXXXXXXXXXXXXXXX

# Approaches to Reach Couterfactual in Special Circumstances
- DID
- RDD
- Instrumental Variable (IV) Estimation

XXXXXXXXXXXXXXXXXXXX [TO BE ENRICHED LATER] 


# ATE and ATT

Suppose $Y$ is an outcome random variable, $A$ is a indicator variable to represent the presence of treatment, for example $A={0,1}$ in binary treatment case. For example, $A=1$ is a condition to represent the diabetes patient population administered the insulin, while $A=0$ is for not administered.

Also, suppose $Y_{a}$ is an outcome when the treatment is SET to $a$; for example, $Y_{a=1}$ is an outcome random variable when the treatment class is $1$ regardless of the actual treatment applied in observing $Y$. This means the random variable $Y_{a=1} | A=0$ can exist and this represents the 'what-if' random variable $Y$ in a sense that it is the random variable under the condition of not being treated ( $A=0$ ) but what if it was treated ( $a=1$ ).

For example, $Y_{a=1} | A=0$ can give the random variable of *HbA1C* for the patient group who was not administered the insulin but in the case if they had been administered. 

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

$<br \ >$

## Rondomized control trial

If the treatment assignment is randomly controlled, the assignment of $A$ is random, *ATE* is equivalent to

$\mathbb{E}[Y|(A=1) \ - \ Y|(A=0)] \ = \ \mathbb{E}[Y|(A=1)] \ - \ \mathbb{E}[Y|(A=0)]$.

In the insulin example, this happens when the patients given insulin are the ones selected randomly with no influence from any attributional factors such as the disease severity, age, or etc. In this situation, we can get the unbiased estimate of effect of insulin by just taking the average of difference of *HbA1C* in the population assigned to treatment group and that in the population assigned to non-treatment group.

$<br \ >$

Here's the proof of this property:

When $A$ is assigned randomly, $Y_{a} \perp A$ for $a \ \in \ \{0,1\}$. This leads to:

$Y_{a=1} \ = \ Y_{a=1}|(A=1) \ = \ Y_{a=1}|(A=0)$ and $Y_{a=0} \ = \ Y_{a=0}|(A=0) \ = \ Y_{a=0}|(A=1)$, (also known as *exchangeability*).

Here, under the RCT set up, we can say the assignment of treatment/non-treatment group $A=a'$ is equivalized to the use of set notation $Y_{a=a'}$ (in RCT, two groups of sujects are 'forced' to comply the individual assignment).

This should result in:

$Y_{a} \ = \ Y$ for $a=$ 0 or 1. (also known as *consistency*)

$<br \ >$

Therefore,

$ATE$

$= \ \mathbb{E}[Y_{a=1} \ - \ Y_{a=0}]$

$= \ \mathbb{E}[Y_{a=1}] \ - \ \mathbb{E}[Y_{a=0}]$

$= \ \mathbb{E}[Y_{a=1}|A=1] \ - \ \mathbb{E}[Y_{a=0}|A=0]$

$= \ \mathbb{E}[Y|A=1] \ - \ \mathbb{E}[Y|A=0]$

$= \ treatment \ effect \ calculated \ in \ RCT$

Wher the third line to the fourth uses *exchangeability* and the four to the fifth uses *consistency*.

Now, it proves the $ATE \ = \ treatment \ effect \ calculated \ in \ RCT$

$<br \ >$

This indicates that under the RCT set up, it is possible to say that the difference in plain averages of each groups (treatment/non-treatment (control)) directly becomes the unbiased estimate of the ATE.

$<br \ >$

Although this is true, it is not always possible to do RCT in real life for various reasons in costs, ethics, and etc., as well as there is already a lot of data collected through non-RCT context ready for being utilized without further data collection efforts. That is why the studies in how to get the value of treatment effect through observational data are appreciated. 

$<br \ ><br \ >$

# Inverse Probability Weighting

When we can get the probabilities of the assignment, i.e. $P[A=1]$ and $P[A=0]$, it is possible to get the unbiased estimate of *ATE* and *ATT*. This method is called Inversed Probability Weighting.

$<br \ >$

# Reference

- "Causal Inference: What If", Miguel A. Hernan, James M. Robins, CRC Press, https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/

