# ananyadas_bitsom_ba_2511216_part2_kpi_experiment

# 1. Task 1: Business Problem Statement

## Background

The company has launched a new onboarding and activation campaign for its subscription-based digital product. Users were randomly assigned to one of two groups:

* **Control Group:** Existing onboarding experience
* **Treatment Group:** New onboarding and activation campaign

## Business Problem

The primary business decision is whether the new onboarding and activation campaign should be rolled out to all users or whether the existing onboarding experience should remain in place.

This decision impacts:

* New users experiencing the onboarding journey
* Product and Growth teams responsible for user activation
* Revenue and Subscription teams responsible for conversion performance
* Company leadership responsible for growth and investment decisions

## Success Metrics

The campaign aims to improve user conversion and early engagement. Key success metrics include:

### Primary Metrics

* Conversion rate from signup to paid subscription
* User activation rate
* Onboarding completion rate

### Secondary Metrics

* Number of sessions during the first week
* Feature adoption rate
* Early user engagement metrics

## Risks and Guardrail Metrics

While increasing conversion and engagement, the company must ensure the new experience does not negatively impact the user experience.

Key guardrail metrics include:

* User churn rate
* Subscription cancellation rate
* Onboarding abandonment rate
* Customer support ticket volume
* Time required to complete onboarding
* Revenue quality and retention metrics

## Evidence Required for Recommendation

Before recommending a full rollout, the analysis must demonstrate that:

1. The Treatment group outperforms the Control group on primary success metrics.
2. The improvement is statistically significant and unlikely to be caused by random variation.
3. No guardrail metrics show meaningful deterioration.
4. The business impact is large enough to justify implementation costs and operational changes.

## Decision Criteria

The Treatment experience should be recommended for rollout only if it delivers measurable, statistically reliable improvements in conversion and engagement while maintaining acceptable performance across all guardrail metrics.

# 2. Dataset Description

## Dataset Link: https://drive.google.com/drive/folders/1AONQ3QSPVvn-A2bWANT0bFtljK1_PSTS
## Overview

The dataset contains user-level experiment data collected from an A/B test designed to evaluate a new onboarding and activation campaign for a subscription-based digital product.

Users were randomly assigned to one of two groups:

* **Control Group:** Existing onboarding experience
* **Treatment Group:** New onboarding and activation campaign

The dataset was used to evaluate whether the Treatment experience improved user conversion, engagement, and revenue outcomes while maintaining acceptable guardrail metrics.

## Dataset Size

* Total Records: **1,408 users**
* Duplicate User IDs Identified: **8**
* Final Analytical Dataset: **1,400 unique users**

## Key Variables

The dataset includes information related to:

### User Information

* User ID
* Region
* Device Type
* Traffic Source
* Plan Type

### Funnel Progression Metrics

* Landing Page Visit
* Trial Started
* Onboarding Completed
* Converted to Paid

### Business Metrics

* Revenue (30-Day Revenue)
* Refund Requested
* Support Ticket Indicator

### Engagement Metrics

* Engagement Score
* Days to Convert

## Analysis Objective

The dataset was analyzed to determine whether the new onboarding campaign generated a statistically significant improvement in paid conversion rate and whether any negative effects were observed through guardrail metrics such as refunds, support tickets, engagement, and revenue quality.


# 3. TASK 3: North Star Metric

## Selected North Star Metric

**Signup-to-Paid Subscription Conversion Rate**

The North Star Metric for this experiment is the percentage of users who convert from signup to a paid subscription after experiencing the onboarding flow.

This metric was selected because it directly measures the business objective of increasing revenue through user conversion. As a subscription-based company, long-term growth depends on the ability to turn new users into paying customers. Improvements in conversion rate indicate that the onboarding and activation experience is effectively communicating product value and motivating users to subscribe.

### Supporting Metrics

The following metrics support the North Star Metric by helping explain user behavior throughout the onboarding journey:

* Activation Rate
* Onboarding Completion Rate
* First-Week Engagement
* Feature Adoption Rate

These metrics provide insights into why conversion changes occur but do not directly represent business success. Therefore, they are treated as supporting metrics rather than the primary success metric.

### Risks of Focusing Only on Conversion

Optimizing conversion rate without considering user experience can lead to:

* Increased churn and cancellations
* Lower-quality subscriptions
* Poor customer satisfaction
* Reduced long-term retention

For this reason, conversion rate must be evaluated alongside guardrail metrics such as churn, cancellation rate, and customer support volume.

# 4. TASK 4: KPI Tree Summary

The KPI tree maps the relationship between the North Star Metric and the key business drivers that influence subscription conversion.

### North Star Metric

* Signup-to-Paid Subscription Conversion Rate

### Primary KPI Drivers

#### 1. User Acquisition Quality

Measures whether incoming users match the target audience and have a high likelihood of becoming subscribers.

Sub-drivers:

* Qualified Signups
* Target Audience Match

#### 2. Onboarding Completion

Measures how effectively users progress through the onboarding experience and reach activation milestones.

Sub-drivers:

* Onboarding Completion Rate
* Time to Activation

#### 3. Early Product Engagement

Measures user interaction with the product during the critical early usage period.

Sub-drivers:

* First-Week Sessions
* Feature Adoption Rate

### Guardrail Metrics

To ensure sustainable growth, the following guardrail metrics are monitored:

* Churn Rate
* Cancellation Rate
* Customer Support Tickets

### Business Insight

The KPI tree demonstrates that higher subscription conversion is achieved by attracting qualified users, helping them successfully complete onboarding, and encouraging meaningful early engagement. At the same time, guardrail metrics ensure that improvements in conversion do not negatively impact retention, customer satisfaction, or long-term business performance.

# 5. Task 5: Clean and Prepare Experiment Data

## Dataset Overview

The experiment dataset contains **1,408 user records** across Control and Treatment groups and includes user acquisition, onboarding, conversion, revenue, and engagement metrics.

## Data Quality Checks Performed

### 1. Missing Values

The dataset was checked for missing values across all columns.

| Column           | Missing Values |
| ---------------- | -------------- |
| device_type      | 18             |
| traffic_source   | 24             |
| engagement_score | 14             |
| days_to_convert  | 1,336          |

#### Handling

* **days_to_convert** is expected to be missing for users who did not convert to a paid subscription and was therefore retained.
* Missing values in **device_type** and **traffic_source** were retained and treated as an "Unknown/Missing" category during segmentation analysis.
* Missing values in **engagement_score** were reviewed and represented less than 1% of the dataset. These records were retained because they do not materially affect experiment outcomes.

---

### 2. Group Counts

The experiment groups were checked to ensure a reasonably balanced randomization.

| Group     | Users |
| --------- | ----- |
| Control   | 693   |
| Treatment | 715   |

#### Result

The allocation is close to a 50/50 split and does not indicate any major randomization issues.

---

### 3. Duplicate User IDs

A duplicate check was performed on the `user_id` field.

#### Result

* Duplicate User IDs Found: **8**

#### Handling

Duplicate records should be removed before conducting final experiment analysis to ensure each user contributes only one observation to the experiment.

---

### 4. Invalid Binary Values

The following binary fields were validated:

* visited_landing_page
* started_trial
* completed_onboarding
* converted_to_paid
* refund_requested

#### Result

All binary columns contained only valid values:

* 0 = No
* 1 = Yes

No invalid values were detected.

---

### 5. Revenue Outlier Detection

Outliers were assessed for the `revenue_30d` variable using the Interquartile Range (IQR) method.

#### Findings

* Majority of users generated zero revenue.
* Maximum observed revenue: **8,610.72**
* Approximately **72 records** were identified as potential revenue outliers.

#### Handling

Revenue outliers were retained because they may represent legitimate high-value customers. Removing them could distort business impact calculations. Sensitivity analysis can be performed later if necessary.

---

### 6. Segment Distribution Across Groups

To verify successful randomization, key user segments were compared between Control and Treatment groups. Available in sheet `Data_Cleaning_Summary`

#### Region Distribution

| Region | Control | Treatment |
| ------ | ------- | --------- |
| North  | 203     | 180       |
| South  | 184     | 184       |
| East   | 158     | 172       |
| West   | 148     | 179       |

#### Device Type Distribution

| Device  | Control | Treatment |
| ------- | ------- | --------- |
| Mobile  | 428     | 436       |
| Desktop | 200     | 214       |
| Tablet  | 56      | 56        |
| Missing | 9       | 9         |

#### Traffic Source Distribution

| Source      | Control | Treatment |
| ----------- | ------- | --------- |
| Organic     | 246     | 241       |
| Paid Search | 156     | 176       |
| Social      | 130     | 133       |
| Referral    | 81      | 91        |
| Email       | 74      | 56        |
| Missing     | 6       | 18        |

#### Result

Segment distributions are generally balanced across experiment groups, suggesting that random assignment was successful and there is no major allocation bias.

---

## Data Preparation Summary

Before analysis:

1. Missing values were reviewed and documented.
2. Duplicate user IDs were identified for removal.
3. Binary fields were validated.
4. Revenue outliers were assessed and retained.
5. Segment balance across Control and Treatment groups was verified.

The dataset is sufficiently clean and appropriate for experiment analysis after removing duplicate user records.

# 6. Task 6: Hypothesis Test Summary

## Objective

The purpose of the hypothesis test was to determine whether the new onboarding and activation campaign (Treatment) significantly improved the paid conversion rate compared to the existing onboarding experience (Control).

## Metric Tested

**Paid Conversion Rate**

Definition:

```text
Paid Conversion Rate = Users Converted to Paid / Total Users
```

This metric was selected as the North Star Metric because it directly measures the company's primary business objective of increasing subscription revenue.

## Hypotheses

### Null Hypothesis (H₀)

The Treatment onboarding experience does not improve the paid conversion rate.

```text
H₀: Treatment Conversion Rate ≤ Control Conversion Rate
```

### Alternative Hypothesis (H₁)

The Treatment onboarding experience improves the paid conversion rate.

```text
H₁: Treatment Conversion Rate > Control Conversion Rate
```

## Test Method

A **Two-Sample t-Test Assuming Unequal Variances** was conducted using the binary `converted_to_paid` variable (0 = not converted, 1 = converted).

The test was performed at a significance level of:

```text
α = 0.05
```

## Results

| Statistic          | Value     |
| ------------------ | --------- |
| P-value            | 0.00054   |
| Significance Level | 0.05      |
| Decision           | Reject H₀ |

Since the p-value (0.00054) is significantly lower than the significance level (0.05), the null hypothesis is rejected.

## Business Interpretation

The results provide strong statistical evidence that the Treatment onboarding experience generated a higher paid conversion rate than the Control experience.

The probability that the observed improvement occurred due to random chance is extremely low. Therefore, the new onboarding campaign appears to be more effective at converting users into paying subscribers.

## Conclusion

Based on the hypothesis test results, the Treatment experience demonstrates a statistically significant improvement in the primary success metric. Subject to validation of guardrail metrics such as refund rate, support ticket rate, engagement score, and revenue impact, the results support consideration of a broader rollout of the new onboarding and activation campaign.

# 7. Task 8: Guardrail metrics considered

# Guardrail Metrics Summary

To ensure that the experiment recommendation was not based solely on conversion improvement, several guardrail metrics were evaluated.

| Metric                   | Control | Treatment | Assessment                          |
| ------------------------ | ------- | --------- | ----------------------------------- |
| Refund Rate              | 0.00%   | 0.42%     | Slight increase, low risk           |
| Support Ticket Rate      | 9.28%   | 16.06%    | Significant increase, high risk     |
| Average Days to Convert  | 8.86    | 6.40      | Faster conversion, positive outcome |
| Average Engagement Score | 57.03   | 62.94     | Higher engagement, positive outcome |
| ARPU                     | 51.97   | 54.25     | Improved revenue quality            |

### Key Findings

* The Treatment group converted users more quickly than the Control group.
* User engagement increased under the new onboarding experience.
* Average Revenue Per User improved, indicating stronger revenue generation.
* Refund requests increased slightly but remained low overall.
* Support ticket volume increased substantially, representing the primary guardrail risk identified during the experiment.

### Overall Assessment

The Treatment experience delivered meaningful business improvements across conversion-related and revenue-related metrics. While the increase in support tickets warrants further investigation, the overall guardrail evaluation suggests that the conversion gains are supported by stronger engagement and revenue outcomes.

The support ticket increase should be monitored closely if the Treatment experience is rolled out more broadly.
# 8. Final Recommendation

## Recommendation

Based on the experiment analysis, I recommend proceeding with a phased rollout of the new onboarding and activation campaign.

### Supporting Evidence

#### 1. Statistically Significant Improvement in Conversion

The hypothesis test produced a p-value of **0.00054**, which is substantially below the significance level of 0.05.

As a result, the null hypothesis was rejected, indicating strong statistical evidence that the Treatment experience improved the paid conversion rate compared with the Control experience.

#### 2. Improved User Engagement

The Treatment group achieved a higher average engagement score:

* Control: 57.03
* Treatment: 62.94

This suggests that users interacted more actively with the product after onboarding.

#### 3. Faster User Activation

The average time required to convert decreased significantly:

* Control: 8.86 days
* Treatment: 6.40 days

Users reached subscription decisions more quickly under the new onboarding experience.

#### 4. Higher Revenue Generation

Average Revenue Per User (ARPU) increased:

* Control: 51.97
* Treatment: 54.25

This indicates that conversion improvements translated into stronger revenue outcomes.

### Risks Identified

The primary concern identified during the experiment was an increase in support ticket volume:

* Control: 9.28%
* Treatment: 16.06%

This suggests that some users may experience confusion or friction within the new onboarding flow.

Refund rates increased slightly from 0.00% to 0.42%, but the overall level remains low and does not currently represent a major business risk.

### Recommended Action

Rather than an immediate full rollout, the company should:

1. Proceed with a phased rollout of the Treatment experience.
2. Investigate onboarding steps that may be generating additional support requests.
3. Monitor support ticket volume and refund rates during rollout.
4. Continue tracking conversion rate, engagement, and revenue quality after launch.

Based on the overall evidence, the business benefits of the Treatment experience outweigh the identified risks.

---

#9. Assumptions and Limitations

## Assumptions

The analysis assumes that:

* Users were randomly assigned to Control and Treatment groups.
* Experiment tracking and event logging were accurate.
* Duplicate user records were successfully removed before analysis.
* Revenue and conversion data accurately reflect user behavior.
* The experiment period was representative of normal business operations.

## Limitations

### 1. Support Ticket Root Cause Unknown

Although support ticket volume increased significantly in the Treatment group, the dataset does not provide ticket categories or reasons. Therefore, the specific onboarding issues causing additional support demand cannot be identified.

### 2. Short-Term Measurement Window

The experiment focuses primarily on early conversion and engagement metrics. Long-term retention and lifetime value were not available for evaluation.

### 3. Refund Rate Sample Size

Refund activity was relatively low across both groups. Small changes in refund counts may produce noticeable percentage differences.

### 4. Segment-Level Constraints

Segment analysis was performed across Region, Device Type, and Traffic Source. However, some segment groups may contain smaller sample sizes, limiting statistical confidence at the segment level.

### 5. External Factors

The analysis assumes that external conditions such as marketing activity, seasonality, and traffic quality remained consistent across both groups during the experiment.

---

# Screenshots Included

The following supporting evidence has been included in the repository:

| File                                   | Purpose                                      |
| -------------------------------------- | -------------------------------------------- |
| screenshots/kpi_tree_preview.png       | KPI tree visualization                       |
| screenshots/hypothesis_test_output.png | Statistical test output and p-value evidence |
| screenshots/summary_metrics.png        | Control vs Treatment summary table

These screenshots provide visual evidence supporting the KPI framework and hypothesis testing results used to make the final recommendation.
