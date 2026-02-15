# A Quantitative Application of Behavioral Economics (Prospect Theory & Mental Accounting)

## Project Overview

This research explores the decision-making mechanisms of Generation Z in Vietnam, applying the principles of **Prospect Theory** and **Mental Accounting**. The core objective is to investigate whether Gen Z exhibits the same risk-taking behaviors when dealing with financial resources (Money) compared to temporal resources (Time).

The study reveals a fascinating psychological asymmetry: Gen Z is significantly more willing to take risks with their money than with their time.

To recreate the result, first need to install dependencies using `pip`: `pip install requirements.txt`

## Core Objectives

1. **Resource Comparison:** Does Gen Z accept more risk with their wallets or their schedules? 


2. **The Probability Effect:** Does the allure of small probabilities (Longshot Bias) apply equally to time and money? 


3. **Personal Consistency:** Is self-assessed personality ("Risk-taker" vs. "Cautious") a reliable predictor of actual behavior, or is it overridden by context? 



## Data Preprocessing Pipeline

Raw data was collected via Google Forms and exported as an Excel spreadsheet. The data preparation pipeline was built using `pandas` and `numpy`, executing the following steps:

* **Column Standardization:** Verbose, full-sentence question headers were mapped to standardized, code-friendly identifiers (e.g., `1. Tình huống 1 - Tiền (Lợi ích, xác suất nhỏ)` converted to `Q1_Money_Gain_Small`) .


* **Data Cleaning:** The `Age` column contained inconsistent string inputs (e.g., "21 tuổi" mixed with integers). A custom string manipulation function extracted isolated numeric digits to standardize the variable as integers .


* **Binary Encoding:** Qualitative text choices were transformed into quantitative binary indicators for risk behavior. Responses indicating absolute certainty ("chắc chắn") were encoded as **0** (Risk Averse). Responses involving chance ("khả năng" or "%") were encoded as **1** (Risk Seeking) .


* **Feature Engineering (Risk Scores):** Two aggregated metrics, `Risk_Score_Money` and `Risk_Score_Time` (ranging from 0 to 4), were computed by summing the binary responses of the four respective scenarios for each resource .



## Statistical Framework

The hypothesis testing was strictly conducted using the `scipy.stats` library. The significance level was set at the standard threshold of 0.05 , with interpretations also acknowledging marginal significance between 0.05 and 0.1.

The following tests were applied:

* **Paired Sample T-test (`scipy.stats.ttest_rel`):** Deployed for Hypotheses 1 and 2 to evaluate within-subject variances. This measured the psychological shift when the *same individual* evaluated identical probability conditions across different resources (Money vs. Time) or probability shifts (5% vs. 50%) .


* **Independent Sample T-test (`scipy.stats.ttest_ind`):** Applied for Hypotheses 3 and 4 to compare the means of two distinct groups (Self-assessed "Cautious" vs. "Risk-taker"). To account for the unequal sample sizes between the two groups, Welch's t-test was utilized by passing the parameter `equal_var=False` .


* **Pearson Correlation Coefficient (`scipy.stats.pearsonr`):** Used for Hypothesis 5 to quantify the linear relationship and behavioral consistency between an individual's total financial risk score and their temporal risk score . Data visualizations for correlations and distributions were generated using `matplotlib` and `seaborn` .



## Hypotheses & Key Findings

### H1: Difference in Risk Tolerance (Money vs. Time)

* **Finding:** Supported at 50% probability.


* **Insight:** In a 50/50 chance to gain a benefit, 50.9% took the risk for Money, but only 34.5% took the risk for Time. The Paired T-test confirmed this shift is statistically significant (p-value = 0.0486). Gen Z views time as irreplaceable; the risk of losing time creates more psychological pressure than failing to earn extra cash.



### H2: The Probability Effect (5% vs. 50%)

* **Finding:** Supported for Gains, Rejected for Losses .


* **Insight:** In gain domains, the rate of choosing risk dropped drastically from 69.1% (at 5% probability) to 50.9% (at 50% probability) for money (p-value = 0.0401). Gen Z falls for the "Longshot Bias" in gains, highly attracted to small probabilities with big rewards. However, in loss domains, the p-values were strictly greater than 0.05, proving sensitivity to probability disappears when facing penalties.



### H3 & H4: Self-Assessed Personality vs. Actual Behavior

* **Finding:** Mostly Rejected .


* **Insight:** Using Welch's independent t-test, self-proclaimed "Risk-takers" only acted significantly riskier than "Cautious" people when dealing with small-probability financial gains (88.2% vs 60.5%, p-value = 0.0189). In **Loss Domains** (facing financial penalties or delayed deadlines), p-values ranged from 0.28 to 0.81, showing fear erased all personality boundaries. Everyone panicked and acted equally cautiously.



### H5: Consistency Across Resources

* **Finding:** Rejected (Pearson r = 0.0576, p-value = 0.6764).


* **Insight:** There is absolutely no linear correlation between how someone risks money and how they risk time. A customer who spends money freely is not necessarily patient. This confirms Thaler's "Mental Accounting" theory—Gen Z keeps Time and Money in completely separate psychological accounts.



## Managerial Implications for Business

Based on our quantitative analysis, we propose three strategies for businesses targeting Gen Z:

1. **Gamify Money, but Guarantee Service:** Use blind boxes and flash sales (small probability/high reward) for financial discounts, but use strict, guaranteed SLAs ("Delivery in 30 mins or your money back") for time-related services .


2. **Behavioral Segmentation > Survey Segmentation:** Traditional personality surveys are flawed predictors of behavior (especially in loss scenarios). Businesses must segment users based on actual historical interaction data.


3. **Monetize Certainty:** Because time and money are not linear substitutes, businesses can successfully sell "Priority Passes" or "Fast Tracks". Gen Z is willing to pay a premium financial price to buy temporal certainty.
