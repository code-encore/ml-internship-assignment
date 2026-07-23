# Capstone Report — <Refresh / Content Opportunity Scoring>

- **Author:*Anuj Pratap Singh*
- **Lane:*Refresh / Content Opportunity Scoring*
- **Repo:*https://github.com/code-encore/ml-internship-assignment/tree/main*
- **Date:*23 JULY 2026*.

## 1. Problem framing

This project supports the decision of which content pages should be prioritized for refresh and review. The unit of analysis is an individual content page. The output is a ranked Refresh Opportunity Score that orders pages from highest to lowest refresh priority.

The intended user is a content strategist, SEO analyst, or editor responsible for maintaining a large content library. Pages with higher scores are reviewed first, while pages with lower scores can be monitored or protected.

A wrong decision has two primary costs:

Refreshing a page that does not need intervention wastes editorial resources.

Missing a page that is declining may result in lost visibility and engagement.

Machine learning helps because large content libraries contain thousands of pages with multiple performance signals. Manual review does not scale well, while a ranking model can consistently identify patterns associated with declining performance.

## 2. Data safety

This project uses anonymized FlyRank warehouse data derived from content performance and search visibility signals.

Included feature categories:

Historical impressions

Historical clicks

Content age

Search visibility indicators

Trend-related metrics

Aggregated performance signals

Excluded fields:

Client identifiers

Client-specific metadata

URLs

Domains

Search queries

Any direct identifying information

Leakage risks considered:

trend_direction was treated as a target-related field and was not used as a predictive feature where it would directly reveal the label.

trend_pct was excluded from model inputs when it was derived from the target outcome.

Client and content IDs were used only for grouping and indexing and never as predictive features.

No client-identifying information appears anywhere in the notebooks, outputs, repository, or final report.
## 3. Baseline

The baseline approach uses a simple rule-based prioritization strategy.

Pages are ranked according to observed performance decline indicators and historical trend signals without machine learning.

This baseline is a fair comparison because:

It uses the same data available to the model.

It reflects a realistic manual prioritization process.

It provides a transparent benchmark.

Baseline Results:

Metric	Baseline
Precision@10	<client353>
Precision@20	<client433>
Recall	<43334>
The machine learning model is evaluated on the same split and metric definitions.
## 4. Model / analysis
A Random Forest model was selected because it performs well on tabular business datasets, handles nonlinear relationships, and provides interpretable feature importance estimates.

Feature list:

impressions_90d

clicks_90d

content_age_days

historical visibility indicators

aggregated performance metrics

trend-related performance signals

engagement-related signals (where available)

Excluded features:

client_id

content_id

target-derived fields

leakage-prone trend outputs

Target Definition:

A Refresh Opportunity Score was created to identify pages showing weaker performance trajectories and therefore higher refresh priority.

The task is treated as a ranking problem rather than a causal prediction problem.
## 5. Evaluation

The dataset was divided into training and testing partitions before evaluation.

Validation Approach:

Train/Test Split

Consistent feature engineering across both sets

Leakage audit before training

Baseline comparison on identical data

Metrics:

Precision@K

Ranking quality

Baseline lift

Results:

Method	Precision@10
Baseline	<fill>
Random Forest	<fill>
Error Analysis:

Most errors occurred among pages with moderate performance signals. These pages often exhibited mixed behavior where historical indicators provided conflicting evidence.

The model performed best on pages with strong positive or negative performance patterns and was less certain for borderline cases.

## 6. Interpretation

The model identified several signals consistently associated with refresh opportunities.

Most Important Features:

Historical impressions

Historical clicks

Content age

Visibility indicators

Trend-related performance signals

Interpretation:

Older content with weakening visibility tended to receive higher refresh scores.

Pages maintaining strong visibility were generally ranked as lower priority.

Content age alone was not sufficient; performance signals provided additional discrimination.

Negative Findings:

Some signals contributed less than expected and did not materially improve ranking quality when added to the model.

This highlights the importance of evaluating features rather than assuming importance.
## 7. Recommendation

The model produces a ranked action list for content teams.

Refresh Immediately
Characteristics:

High refresh score

Declining visibility

Weak recent performance

Recommended Actions:

Update content

Expand coverage

Improve internal linking

Review metadata

Review and Optimize
Characteristics:

Moderate refresh score

Mixed performance signals

Recommended Actions:

Improve title and metadata

Review structure

Monitor performance trends

Monitor
Characteristics:

Stable performance

Recommended Actions:

Periodic review

Continue observation

Protect
Characteristics:

Strong visibility

Positive performance trajectory

Recommended Actions:

Avoid unnecessary modifications

Preserve successful structure

Confidence:

The recommendations are intended as decision-support guidance rather than guarantees of future performance.
## 8. Reproducibility

Repository Structure:

work/
├── notebooks/
│   ├── w01_research_question.ipynb
│   ├── w02_ml_task_framing.ipynb
│   ├── w03_data_contract.ipynb
│   ├── w04_signal_audit.ipynb
│   ├── w04_baseline_score.ipynb
│   ├── w05_model.ipynb
│   ├── w06_validation_audit.ipynb
│   └── capstone.ipynb

Run Order:


jupyter notebook

Run:
1. w01_research_question.ipynb
2. w02_ml_task_framing.ipynb
3. w03_data_contract.ipynb
4. w04_signal_audit.ipynb
5. w04_baseline_score.ipynb
6. w05_model.ipynb
7. w06_validation_audit.ipynb
8. capstone.ipynb


Random Seed:

RANDOM_SEED = 42

nvironment:

Python 3.11+

pandas

numpy

scikit-learn

matplotlib

seaborn (if used)

jupyter

Requirements should be stored in:

requirements.txt
> **Claims checklist before submitting:*
✔ Observational analysis only
✔ Decision-support system
✔ No causal claims
✔ No client-identifying information
✔ No Google algorithm claims
✔ Reproducible workflow
✔ Baseline comparison included
✔ Ranking-focused evaluation included* observed / measured / directional / decision-support
> **Metrics vs. base rate:*Precision@K

Ranking quality

Baseline lift*

 report your task's base rate (majority-class %) next to any