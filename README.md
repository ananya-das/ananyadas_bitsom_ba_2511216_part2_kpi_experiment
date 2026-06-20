# ananyadas_bitsom_ba_2511216_part2_kpi_experiment

# Task 1: Business Problem Statement

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

# TASK 2: North Star Metric

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

# TASK 3: KPI Tree Summary

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

# Task 4: Clean and Prepare Experiment Data

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
