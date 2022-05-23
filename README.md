# Why Does Causality Analysis Matter?

Here we define the *Causality Analysis* as a field of study to establish the relationship between cause and effect from the data. Why does it matter though?

In a sentence, that is because **"correlation does not indicate the causation"**.

<a href="https://www.wnycstudios.org/podcasts/otm/articles/spurious-correlations">Deaths by Swimming Pool Drowning vs. Nicholas Cage Films</a> a famous example of this statement.

![](https://i.imgur.com/q54sO25.png)

Although "the number of people who drowned by falling into the swimming pool" is correlated with "the number of films Nicolas Cage appeared in", it does not mean they have a causal relationship (no proof, but just by common sense!)

Therefore, this is an easy example of correlation != causation, period.

$<br \ >$

Although it is true, there is a further implication in the data science field: it matters when we want to know the **influence of the actions changing a part of the system**. In the example above, <ins>decreasing the Nicolas Cage's films does not lead to a decrease in the pool accidents</ins> (again no proof but in common sense.)

But there are many cases where this kind of effect is what we want to know, for example:
- how likely can a patient be treated if the doctor administered a drug,
- how likely do we see more conversions if a marketing campaign went live,
- how likely can the city gain more budget when a tax policy was enforced,
- etc.

This is also known as *do-operator* in the causality analysis <a href="http://mlg.eng.cam.ac.uk/zoubin/tut06/cambridge_causality.pdf">(a reference here)</a> like $E[Y=y | A]$ vs. $E[Y=y | do(A)]$. No matter how it is called, this difference is something we should carefully concern and distinguish.


$<br \ ><br \ >$

# Concept of Counterfactual

In *causality analysis*, smacking *counterfactual* property of the real world is the key approach to measure the effect in our interest.

Imagine that we have sent out campaign emails to selected customer groups (by the possible propensity of positive reaction, etc.). We have two customer groups: one who received the mail, the other who didn't. Each of them returns some responses to the mail.

![](./data/image/counterfactual_1.jpg)

In this exhibit, we only have the data for *(1)* and *(4)*. Unfortunately, the difference between *(1)* and *(4)* does not represent the causal effect in general and is biased. This is because when we send a campaign mail, we already see the customers' attributes, past sales, etc., and cherry-pick them. The customers we send the mail are possibly the customers who are already likely to respond positively. If that is the case, the campaign effect is overestimated.

![](./data/image/counterfactual_2.jpg)

What we want to know is the difference between *(1)* and *(2)*, not *(4)*, and/or between *(3)* and *(4)*, not *(1)*. With that information, we can discuss whether the campaign mail has done the expected job.

Since the information of *(2)* and *(3)* does not appear in the real world, it is called <b><ins>counterfactual</ins></b>. 

A guru of causality analysis, Donald Rubin called this counterfactual aspect of the observed data "the fundamental problem of causal inference" <a href="https://en.wikipedia.org/wiki/Rubin_causal_model#The_fundamental_problem_of_causal_inference">(Wikipedia)</a>

$<br \ >$

As discussed later, RCT is one possible approach to overcome this problem and a method highly ranked in the hierarchy of the strength of the evidence in the scientific research <a href="https://en.wikipedia.org/wiki/Hierarchy_of_evidence">("Hierarchy of evidence")</a>, yet because RCT is not always possible to conduct, the importance of causality analysis still remains. We will discuss more in the later sections.

$<br \ ><br \ >$

# Approaches to Reach Counterfactual in Special Circumstances
- DID
- RDD
- Instrumental Variable (IV) Estimation

XXXXXXXXXXXXXXXXXXXX [TO BE ENRICHED LATER] 

$<br \ ><br \ >$

# ATE (Average Treatment Effect) and ATT (Average Treatment Effect of the Treated)

Suppose $Y$ is an outcome random variable and $A$ is an indicator variable to represent the presence of treatment, for examplem $A \in \lbrace 0,1 \rbrace$ in a binary treatment case. For example, $A=1$ is a condition to represent the diabetes patient population is administered the insulin, while $A=0$ is for not administered.

Also, suppose $Y_{a}$ is an outcome when the treatment is SET to $a$; for example, $Y_{a=1}$ is an outcome random variable when the treatment class is $1$ regardless of the actual treatment applied in observing $Y$. This means the random variable $Y_{a=1} | A=0$ can exist and this represents the 'what-if' value of $Y$ in a sense that it is the random variable under the condition of not being treated ( $A=0$ ) but what if it was treated ( $a=1$ ). 

This random variable $Y_{a=1} | A=0$ is analogous to the cell *(2)* in the matrix of "Concept of Counterfactual" section above.

For example, $Y_{a=1} | A=0$ can give the random variable of *HbA1C* for the patient group who was not administered the insulin but in the virtual case when they had been administered. 

Here the $ATE$ (Average Treatment Effect) and $ATT$ (Average Treatment Effect of the Treated) are introduced.

$<br \ >$

## *ATE* (Average Treatment Effect)

$ATE \ = \ \mathbb{E}[Y_{a=1}-Y_{a=0}]$

This represents the expectation of the effect of the treatment in a sense it takes the difference of the outcome random variables, the former is if the whole population was set in the treatment group while the latter is if set in the non-treatment group.

$<br \ >$

## *ATT* (Average Treatment Effect of the Treated)

$ATT \ = \ \mathbb{E}[Y_{a=1}-Y_{a=0}|A=1]$

This represents the similar expectation of effect to *ATE* with the only difference in the random variable in interest being only from the population who was treated because it is conditioned by $A=1$.

$<br \ >$

## *ATE* vs. *ATT* in an example

Let's describe the difference of *ATE* and *ATT* in English with an example of insulin patient. 

- *ATE* is the expected effect of insulin (e.g. decrease in *HbA1C*) against the entire population in interest.

- *ATT* is the expected effect of insulin against the population who was actually given insulin, and disregarding the population who was not given insulin--supposedly they are severer diabetic patients because the physicians found out they should take the insulin.

$<br \ ><br \ >$

# Rondomized control trial

If the treatment assignment is randomly controlled where the assignment of $A$ is random, the calculation of *ATE* is much easier, because it is equivalent to the average of observed outcomes in each group:

$\mathbb{E}[Y|(A=1) \ - \ Y|(A=0)] \ = \ \mathbb{E}[Y|(A=1)] \ - \ \mathbb{E}[Y|(A=0)]$.

In the insulin example, this happens when the patients given insulin are selected randomly with no influence from any attributional factors to the selection process such as the disease severity, age, etc. In this situation, we can get an unbiased estimate of the effect of insulin by just taking the average difference of *HbA1C* in the population assigned to the treatment group and that in the population assigned to the non-treatment group.

$<br \ >$

Here's the proof of this property:

------------------

When $A$ is assigned randomly, $Y_{a} \perp A$ for $a \ \in \ \{0,1\}$. This leads to:

$Y_{a=1} \ = \ Y_{a=1}|(A=1) \ = \ Y_{a=1}|(A=0)$ and $Y_{a=0} \ = \ Y_{a=0}|(A=0) \ = \ Y_{a=0}|(A=1)$, (also known as *exchangeability*).

Here, under the RCT setup, we can say the assignment of treatment/non-treatment group $A=a'$ is equalized to the use of set notation $Y_{a=a'}$ (in RCT, two groups of subjects are 'forced' to comply the individual assignment).

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


Where the transform from the second line to the third uses *exchangeability* and from the third to the fourth uses *consistency*.

Now, it proves the $ATE \ = \ treatment \ effect \ calculated \ under \ RCT$

------------------

$<br \ >$

This indicates that under the RCT setup, it is possible to say that the difference in plain averages of each group (treatment/non-treatment (control)) directly becomes the unbiased estimate of the ATE.

$<br \ >$

Although RCT indeed solves the issue in the estimate of treatment effect, it is not always possible to do RCT in real life for various reasons in costs, ethics, etc. Also, let's take the fact into account that there is already a lot of data collected through non-RCT contexts ready for being utilized without further data collection efforts. That is why the studies on how to get the value of treatment effect through observational data are appreciated.

$<br \ ><br \ >$

# Population Bias as A Type of Counterfactuality

The challenge appears though when using observational data. Primarily, the lack of $Y_{a} \perp A$ or *exchangeability* is an issue. In plain English, this means the outcome for the treated group and the outcome for the untreated group are not equivalent. For examples:
- the effect of insulin is not the same to the patients who are administered and the ones who are not; because it depends on the doctors' discretions and the former patient group is supposedly under severer condition than the latter.
- the effect of marketing campaign such as coupon distribution is not the same to the customers who received the coupon and the ones who do not; because it depends on the marketing team's discretion and the former customer group is supposedly promising and sensitive to the campaign than the latter.

In general, this limitation is just called **population bias**. Next section shows one of the possible approaches we can take to tackle this limitation and get the unbiased estimate of the treatment effect.

$<br \ ><br \ >$

# Inverse Probability Weighting

When we can get the probabilities of the assignment, i.e. $P[A=1]$ and $P[A=0]$, it is possible to get the unbiased estimate of *ATE* and *ATT* from the observational data. This method is called Inversed Probability Weighting.

Under the observational data, we have a set of observational data, $\lbrace ( Y_{i}, A_{i} ) \rbrace^{n}_{i=1}$. The Inversed Probability Weighted Estimator (*IPWE*) for $a=a'$ is given by:

$\hat{\mu}^{IPWE}\_{a'} \ = \ \frac{1}{n} \sum\limits_{i=1}^{n} Y_{i} \frac{\boldsymbol{1}\_{A_i=a'}}{P[A_i=a']}$

Where the $\boldsymbol{1}\_{A_i=a'}$ represents an indicator function to give $1$ when $A_i=a'$ and $0$ otherwise.

$<br \ >$

This *IPWE* is an unbiased estimator of $Y_{a=a'}$, namely $\mathbb{E}[\hat{\mu}^{IPWE}\_{a'}] \ = \ Y_{a=a'}$.

Then, we can conclude we can estimate the *ATE* such that




$<br \ >$

Here's the proof of this property:

------------------

XXXXXXXXXXXXXXXXXXXX [TO BE ENRICHED LATER] 

------------------

$<br \ >$



$<br \ ><br \ >$

# Reference

- "Causal Inference: What If", Miguel A. Hernan, James M. Robins, CRC Press, https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/
- "CAUSALITY", Ricardo Silva, Cambridge Advanced Tutorial Lecture Series on Machine Learning, http://mlg.eng.cam.ac.uk/zoubin/tut06/cambridge_causality.pdf

