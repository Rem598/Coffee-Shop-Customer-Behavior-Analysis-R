# ☕ Coffee Shop Customer Behavior Analysis (R)

## 🎯 Problem Statement 

The objective was to leverage customer survey data to **quantify the relationships between visit habits, loyalty status, and overall satisfaction**. The analysis was designed to provide the coffee shop management with **data-driven recommendations** for increasing customer retention and optimizing marketing spend.

**Tools Used:** **R** (Programming Language), **`t.test`**, **`aov` (ANOVA)**, **`chisq.test`**, **`glm` (Logistic Regression)**

---

## 📋 Project Overview

This project analyzes data collected from a customer satisfaction and behavior survey at a coffee shop. The analysis goes beyond basic reporting to employ inferential statistics to test specific hypotheses regarding:

* **Demographics** vs. Visit Frequency ($\chi^2$ Test)
* **Satisfaction** vs. Visit Frequency (ANOVA)
* **Loyalty** vs. Time Spent in Shop (T-test)
* **Likelihood to Recommend** (Logistic Regression for NPS modeling)

---

## 📊 Key Findings & Results

### 1. Descriptive Statistics

* The **mean age** of customers is **40**.
* The primary demographic is balanced, with a slight majority in one gender category (details in ![Gender](https://github.com/Rem598/Coffee-Shop-Customer-Behavior-Analysis-R/blob/main/Gender.png)).

### 2. Product Preferences

Despite being a "coffee shop," the analysis revealed that **tea** was the most preferred product among surveyed customers. This insight provides an opportunity to adjust merchandising or promotional focus.

![Product popularity table](https://github.com/Rem598/Coffee-Shop-Customer-Behavior-Analysis-R/blob/main/Product%20popularity.png)

---

### 3. Visit Frequency & Demographics ($\chi^2$ Test)

The $\chi^2$ test was used to determine if visit frequency is independent of age group and gender.

* **Age Groups:** The analysis involved creating age groups (Teen, Young Adult, Adult, Middle-Aged, Senior). The $\chi^2$ test showed a **statistically significant relationship** between Age Group and Visit Frequency (details in `Age Chi.png`), suggesting habits differ strongly by life stage.
* **Gender:** The test revealed **no statistically significant relationship** between Gender and Visit Frequency (details in `Gender chi.png`).

![Visit Frequency by Age Group Chart](https://github.com/Rem598/Coffee-Shop-Customer-Behavior-Analysis-R/blob/main/Visit%20Freq%20by%20Age%20Group.png)

![Visit Frequency by Gender](https://github.com/Rem598/Coffee-Shop-Customer-Behavior-Analysis-R/blob/main/Visit%20Freq%20by%20Gender.png)

---

### 4. Satisfaction Analysis (ANOVA)

One-way **ANOVA** was used to test if the **mean satisfaction score differed significantly** across various Visit Frequency groups.

```R
anova_freq_sat <- aov(Satisfaction_Score ~ Visit_Frequency, data = coffee2)
summary(anova_freq_sat)
```
![Anova](https://github.com/Rem598/Coffee-Shop-Customer-Behavior-Analysis-R/blob/main/Anova%20one.png)
The resulting ANOVA table  confirmed that satisfaction scores are significantly different based on how often a customer visits.

### 5. Loyalty and Time Spent (T-Test)
A t-test was performed to compare the mean time spent in the shop by loyalty members versus non-members.

```R

t_test_time_loyalty <- t.test(`Time_Spent (min)` ~ Loyalty_Member, data = coffee2)
```
![t-test](https://github.com/Rem598/Coffee-Shop-Customer-Behavior-Analysis-R/blob/main/t-test.png)
The results confirmed a statistically significant difference: Loyalty members spend more time in the shop than non-members, confirming the value of loyalty programs in promoting longer visits and higher potential spend.

### 6. Likelihood to Recommend (Logistic Regression)
Logistic regression was used to model the likelihood of a customer recommending the shop (Would_Recommend is the binary dependent variable), which is a proxy for the Net Promoter Score (NPS).
```R
model_recommend <- glm(Would_Recommend ~ Age + Visit_Frequency + Satisfaction_Score + Loyalty_Member, 
                       data = coffee2, family = binomial)
```
![RecommendLikelihood](https://github.com/Rem598/Coffee-Shop-Customer-Behavior-Analysis-R/blob/main/Recommend.png)
The model summary  shows that Satisfaction Score and Loyalty Status are the most significant predictors of whether a customer will recommend the shop.

💡 Conclusion & Recommendations
The analysis provides a clear road map for management:

- Prioritize Loyalty: Loyalty members are key drivers of longer visits and higher likelihood to recommend. The loyalty program should be prioritized.

- Focus on Frequency: Satisfaction is directly tied to visit frequency; incentives to convert occasional visitors into regulars will boost overall happiness.

- Address Product Insights: The unexpected preference for tea suggests an opportunity to expand or better promote the tea menu to capitalize on the existing demand.
