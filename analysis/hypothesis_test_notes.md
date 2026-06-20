# Hypothesis Testing Notes

## Objective

The objective of this experiment is to determine whether the new onboarding and activation campaign (Treatment) leads to a higher paid conversion rate than the existing onboarding experience (Control).

The results of this hypothesis test will support the business decision of whether the new onboarding campaign should be launched to all users.

---

# Metric Being Tested

## Primary Metric

**Paid Conversion Rate**

Definition:

```text
Paid Conversion Rate = Users Converted to Paid / Total Users
```

This metric was selected because it is the North Star Metric for the experiment and directly measures the company's primary business objective: increasing the number of paying subscribers.

---

# Hypotheses

Let:

* p₁ = Paid conversion rate for the Control group
* p₂ = Paid conversion rate for the Treatment group

## Null Hypothesis (H₀)

The new onboarding campaign does not improve paid conversion.

```text
H₀: p₂ ≤ p₁
```

There is no statistically significant increase in paid conversion rate for users exposed to the Treatment experience.

---

## Alternative Hypothesis (H₁)

The new onboarding campaign improves paid conversion.

```text
H₁: p₂ > p₁
```

Users exposed to the Treatment experience have a higher paid conversion rate than users exposed to the Control experience.

---

# Type of Test

## One-Tailed Test

A one-tailed test is appropriate because the business objective is specifically to determine whether the Treatment performs better than the Control.

The company is not interested in proving that the Treatment performs differently in either direction. The decision criterion is whether the Treatment produces a statistically significant improvement in conversion.

---

# Significance Level

## Alpha (α)

```text
α = 0.05
```

A 5% significance level is used, which is the standard threshold in A/B testing and business experimentation.

This means there is a 5% risk of incorrectly concluding that the Treatment improves conversion when no true improvement exists.

---

# Reason for Choosing This Metric

Paid Conversion Rate was selected because:

* It directly measures business success.
* It is closely tied to subscription revenue.
* It aligns with the experiment objective of improving user activation and conversion.
* It is the primary metric leadership will use when deciding whether to launch the new onboarding experience.

Supporting metrics such as onboarding completion rate, trial start rate, and engagement score help explain user behavior but do not directly represent revenue generation.

---

# Decision Rule

## Reject the Null Hypothesis

Reject H₀ if:

```text
p-value < 0.05
```

This indicates statistically significant evidence that the Treatment increases paid conversion.

---

## Fail to Reject the Null Hypothesis

Fail to reject H₀ if:

```text
p-value ≥ 0.05
```

This indicates insufficient evidence to conclude that the Treatment improves paid conversion.

---

# Interpretation Logic

### Scenario 1: Significant Improvement

If the Treatment group's paid conversion rate is higher than the Control group's rate and the p-value is below 0.05:

* Reject the null hypothesis.
* Conclude that the new onboarding campaign significantly improves conversion.
* Consider recommending a full rollout, provided guardrail metrics remain healthy.

### Scenario 2: No Significant Improvement

If the p-value is greater than or equal to 0.05:

* Fail to reject the null hypothesis.
* Conclude that the observed difference may be due to random variation.
* Do not recommend a full rollout based solely on conversion performance.

### Scenario 3: Significant Improvement but Poor Guardrails

If conversion improves significantly but guardrail metrics worsen substantially:

* Additional analysis is required.
* The business should evaluate trade-offs between growth and user experience before rollout.

---

# Connection to Business Decision

The outcome of this hypothesis test directly determines whether the new onboarding campaign creates measurable business value.

A statistically significant increase in paid conversion rate, combined with acceptable guardrail performance, would provide evidence to support launching the Treatment experience to all users. Conversely, a lack of statistical significance or deterioration in guardrail metrics would suggest retaining the current onboarding experience or conducting further testing.
