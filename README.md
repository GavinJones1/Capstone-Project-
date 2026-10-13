Predicting Sports Injury Occurrence Using Machine Learning Methods and Feature Analysis

Business Analytics Capstone | Kent State University | Presented April 21, 2025

Team: Tyler J. Caplinger, Daniel B. Hanson, Gavin J. Jones

A machine learning study that tests 24 classification models across three feature-set sizes (10, 18, and 25 predictors) to predict whether an athlete will be injured. Models were ranked with a weighted z-score method that puts the most weight on recall, because a missed injury costs more than a false alarm. A decision tree (Model 2.2) ranked first in the 18-variable (medium) feature set.

Table of Contents
Project Overview
Key Findings
Data
Methodology
Weighted Scoring Method
Results
Limitations
Future Work
Repository Contents
Tools
Contact
Project Overview

Injuries affect athlete health, team performance, and cost. Traditional methods rely on observation and self-reported fatigue, and standard statistical models often reach high accuracy while missing the athletes most at risk.

This project asks:

Can machine learning predict injury occurrence from physiological, biomechanical, training, environmental, and demographic data?
Which model performs best when recall (catching real injuries) is the priority?
How does the number of predictors affect performance?
Key Findings
Model 2.2 (decision tree) had the highest weighted score of all 24 models in the medium (18-variable) feature set, driven by the highest recall in the study (83.43%).
Decision trees were the strongest model family. The second-ranked model was also a decision tree (Model 2.3, 81.32% recall).
More features did not mean better performance. The 18-variable set performed best. Moving from 18 to 25 variables lowered accuracy and recall across model types, which points to added noise.
Accuracy alone is misleading here. About 85% of observations are non-injury, so many models landed near 85% accuracy while catching almost none of the injuries (macro recall near 50%).
Higher recall cost precision. The top models caught more injuries but produced more false positives. For injury prevention, the team treated a missed injury as the more costly error.
The most influential predictors in the combined feature ranking were recovery score, sleep quality, and fatigue index, followed by training load.
Data
Item	Detail
Training set	10,820 observations
Test set	1,909 observations
Target	injury_occurred (0 = no injury, 1 = injury)
Class balance	About 85% no injury, 15% injury
Predictors	25 variables in five groups

Predictor groups

Group	Variables
Physiological	heart rate, body temperature, hydration level, sleep quality, stress level, BMI
Biomechanical	joint angles, gait speed, cadence, step count, jump height, ground reaction force, range of motion
Training and workload	training intensity, training duration, training load, fatigue index
Environmental	ambient temperature, humidity, altitude, playing surface
Demographic	age, gender, sport type

Data preparation: The dataset was cleaned before modeling using the Ohio Supercomputer Center with MATLAB. Missing values, outliers, and scaling were handled in that step, so the data was ready for modeling when the team received it. The raw data file is not included in this repository.

Methodology
Feature selection. Every variable was ranked with four methods: Minimum Redundancy Maximum Relevance (MRMR), ANOVA, Chi-Square, and Kruskal-Wallis. The four ranks were averaged into one final ranking.
Three feature sets built from that ranking:
Feature set	Variables	Contents
Small	10	fatigue index, training load, training intensity, heart rate, sleep quality, ground reaction force, joint angles, ambient temperature, humidity, age
Medium	18	the small set plus hydration level, stress level, BMI, gait speed, cadence, range of motion, training duration, playing surface
Large	25	the medium set plus body temperature, step count, jump height, altitude, gender, sport type
Model training. 24 models from six families were trained on each feature set in MATLAB, with 5-fold cross-validation and evaluation on the held-out test set:
Decision trees (fine, medium, and coarse)
Support vector machines (linear, quadratic, cubic, and three Gaussian variants, plus kernel and efficient linear SVMs)
Ensembles (boosted, bagged, and RUSBoosted trees)
Neural networks (narrow, medium, wide, bilayered, and trilayered)
Naive Bayes (Gaussian and kernel)
Logistic regression (binary GLM, efficient, and kernel)
Repeated runs. Each model was run 5 times per feature set to reduce the effect of random variation.
Evaluation and ranking. Models were compared on recall, accuracy, precision, and training time, and ranked with a weighted z-score method.
Weighted Scoring Method

Each metric was converted to a z-score so models could be compared on one scale, then combined using these weights:

Metric	Weight
Recall	50%
Accuracy	20%
Precision	20%
Training time	10%

Recall carries the most weight because a false negative (a missed injury) is the costly error in injury prevention. Training time carries the least and accounts for model efficiency.

Results

Feature-set comparison. Performance improved from the small (10) to the medium (18) feature set and declined from the medium to the large (25) set. The medium set was the most consistent, so the final model ranking uses it.

Top models, medium feature set

Rank	Model	Type	Recall (%)	Precision (%)	Weighted score
1	2.2	Decision tree	83.43	14.43	0.919
2	2.3	Decision tree	81.32	15.58	0.655
3	2.19	Neural network	59.98	75.71	0.434
4	2.7	Naive Bayes	60.08	76.72	0.412
5	2.22	Neural network	62.37	66.48	0.340

Model 2.4 (binary GLM logistic regression) had the lowest weighted score (-0.732). It matched the majority-class baseline, with recall near 50%.

Other feature sets. In the large set, an ensemble (Model 2.17) had the highest recall at about 75%. In the small set, an SVM (Model 2.9) had the highest recall but ranked 9th overall.

Takeaways

Recall should be the lead metric for injury prediction.
Tree-based models were the most effective at identifying injuries.
Feature selection matters: the medium set beat both the small and large sets.
There is a recall-versus-precision tradeoff, and the right balance depends on how a team weighs missed injuries against false alarms.
Limitations
The top-ranked models have low precision, meaning many false positives.
The data was provided pre-processed, so the team could not review how it was collected or cleaned beyond what was documented.
Results come from one dataset and have not been validated on outside data or in a live setting.
Model rankings depend on the chosen weights (50/20/20/10). Different weights could change the order.
Future Work
Validate the best models on new data from other teams, sports, or seasons.
Tune the decision threshold to balance recall against false positives.
Test the models with wearable data (for example WHOOP or Oura) for real-time risk monitoring.
Build a dashboard that gives coaches and athletic trainers daily injury-risk estimates.
Repository Contents
File	Description
README.md	Project summary (this file)
docs/	Full research paper (Word)
presentation/	Capstone presentation slides
results/	MATLAB model results, weighted scores, and feature rankings (Excel)
Tools
MATLAB (Classification Learner) for model training and evaluation
Ohio Supercomputer Center for data cleaning
Excel for results, z-score calculations, and weighted scoring
Techniques: classification, feature selection (MRMR, ANOVA, Chi-Square, Kruskal-Wallis), cross-validation, z-score standardization
Contact

Gavin Jones | M.S. Business Analytics candidate, Kent State University | NCAA Division I Baseball LinkedIn | Gavjones1230@gmail.com
