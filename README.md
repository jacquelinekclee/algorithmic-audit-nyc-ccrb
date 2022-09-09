# Algorithmic Audit: Modeling the New York City Civilian Complaint Review Board and Auditing the Model Fairness

![banner](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/e6fe2eb9f6dbe7af249f0bac74fd1296b2e5d088/Screen%20Shot%202022-09-08%20at%205.37.33%20PM.png)

[CCRB logo](https://www1.nyc.gov/assets/ccrb/images/content/pages/board-members/image_missing.png), [NYPD logo](https://en.wikipedia.org/wiki/New_York_City_Police_Department)

## For Full Paper, [Click Here](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/aa536a7c4a71f71eaf114cd817be665e8a0b5252/paper2.pdf). For Paper Covering The Background/Invesitgation of Inequity (Paper 1), [Click Here](
Please note that this README functions only as an overview of the work done! Please take a look at the final papers (linked above) or their corresponding Python notebooks:
- [Algorithmic Audit Python Notebook Link](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/4120ace9bea5f2d2045f8d984f68f158b23f94f9/Paper%202%20-%20Modeling%20the%20New%20York%20City%20Civilian%20Complaint%20Review%20Board%20and%20Auditing%20the%20Model%20Fairness.ipynb)
- [Inequities in Civilian Complaints to the NYPD Link](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/4120ace9bea5f2d2045f8d984f68f158b23f94f9/Paper%201%20-%20Inequities%20in%20Civilian%20Complaints%20to%20the%20NYPD.ipynb)

# Table of contents

- [Background](#background)
- [Tools Used](#tools-used)
- [The Data](#the-data)
- [The Logistic Regression Model](#the-logistic-regression-model)
- [Overview of Parity Measures and Fairness Results](#overview-of-parity-measures-and-fairness-results)
- [Findings and Conclusion](#findings-and-conclusion)

# Background
This paper and analysis was done during Spring 2022 as part of the course [DSC 167](https://afraenkel.github.io/fairness-algo-decision/): Fairness and Algorithmic Decision Making at UC San Diego's Halıcıoğlu Data Science Institute. The purpose of the assignment and aim of this paper was to find a system or mechanism that has a potential inequity, model the decision making process, and evaluate/audit this model using parity measures and frameworks of distributive justice. I hope that this paper can teach data scientists or those interested in the field about how ethics and fairness come into play in data science and the algorithms us data scientists create. 

The New York City Civilian Complaint Review Board (CCRB), the system in this context, is an agency independent from the New York Police Department that investigates complaints against NYPD officers regarding allegations of excessive or unnecessary force, abuse of authority, discourtesy, or offensive language. Throughout the investigation process, the review board may obtain further evidence from the NYPD (e.g., body camera footage) and conduct interviews of anyone involved to use alongside any details the complainant submitted in their original complaint. Specific complainant/victim attributes collected include age, gender, and ethnicity. The complainant may also provide details on the officers’s sex, race, and physical appearance.

The potential inequity I investigated involves the "disposition" of a given complaint, or the ruling the CCRB determines. A substantiated complaint is one for which the alleged conduct was found to have happened and violated NYPD rules, potentially leading to punishment or repercussions for the accused officer. The data shows that complaints submitted by Black complainants were less often substantiated than non-Black complainants. This discrepancy was the launching pad for my investigation of this inequity and audit of the CCRB. 

[(Back to top)](#table-of-contents)

# Tools Used
- Python
- Jupyter Notebooks
- Scikit Learn for Modelling
- Pandas for Data Cleaning, Exploration, etc.
- NumPy for Data Cleaning, Exploration, etc.
- Matplotlib for Data Visualizations

![tools-used](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/3f42afbac03d36df9b95b891e16dedbd1255dd62/tools_used_pic.png)

[Python logo](https://logos-world.net/wp-content/uploads/2021/10/Python-Symbol.png), [Scikit learn logo](https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Scikit_learn_logo_small.svg/1200px-Scikit_learn_logo_small.svg.png), [Pandas logo](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/2560px-Pandas_logo.svg.png), [NumPy logo](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/NumPy_logo_2020.svg/1280px-NumPy_logo_2020.svg.png), [Jupyter logo](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Jupyter_logo.svg/1200px-Jupyter_logo.svg.png), [Matplotlib logo](https://matplotlib.org/stable/_images/sphx_glr_logos2_003.png). 

[(Back to top)](#table-of-contents)

# The Data
The data originally comes from [ProPublica](https://www.propublica.org/datastore/dataset/civilian-complaints-against-new-york-city-police-officers) and contains information regarding complaints made starting in 1985 up to 2020. The model uses data starting in 2000 because key demographic features like complainant ethnicity were not tracked before then. All complaints include the type of complaint made, the precinct in which the alleged action took place, demographics on the complainant, and demographics on the accused officer. See [allegations.csv](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/ca06036fecf6efa016e9cd8de1fe9637768bffa5/allegations.csv) and [allegations_cleaned.csv](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/ca06036fecf6efa016e9cd8de1fe9637768bffa5/allegations_cleaned.csv).

## Additional Data

Borough was not a column initially included in the dataset, so the precincts were mapped to their apporpriate boroughs using data pulled from the [NYPD's website](https://www1.nyc.gov/site/nypd/bureaus/patrol/precincts-landing.page). See [precinct_boroughs.csv](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/ca06036fecf6efa016e9cd8de1fe9637768bffa5/precinct_borough.csv) 

In order to understand the different categories of complaints and the potential consequences an officer may face, I referenced the [CCRB's rules](https://www1.nyc.gov/assets/ccrb/downloads/pdf/about_pdf/Title38-A_20210526.pdf). This information was used in feature engineering. 

In the first, investigatory paper, data on arrests in NYC and stop, question, and frisk patterns were investigated. Please visit [this link](https://data.cityofnewyork.us/Public-Safety/NYPD-Arrests-Data-Historic-/8h9b-rp9u) for the arrests data and [this link](https://data.cityofnewyork.us/Public-Safety/The-Stop-Question-and-Frisk-Data/ftxv-d5ix) for the stop, question, and frisk data. 

[(Back to top)](#table-of-contents)

# The Logistic Regression Model

A simple logistic regression model with with L2 regularization was used to model the CCRB's decision process. To train the model, a simple 75%-25% train-test split was used. To combat the class imbalance present (only about 25% of complaints were deemed substantiated), the `class_weight` hyperparameter, which assigns a weight to each class that the model uses for penalizing, was used. In order to determine the proper decision thereshold, different utility functions were compared, ultimately leading to a threshold of 0.527 instead of the default 0.5. This means that anything that the model classifies points as substantiated if the resulting regression prediction is at least 0.527. See the paper for more details. 

## Features
The features used in the model are `contact_reason` (or text indicating why the officer approached the civilian), `mos_ethinicity` (officer’s ethnicity), rank_incident (officer’s rank at time of incident), `mos_gender` (officer’s gender), `complainant_gender` (complainant’s gender), `mos_age_incident` (officer’s age at time of incident), `complainant_age_incident` (complainant’s age at time of incident). `borough` (the borough in which the incident took place), `black` (whether the complainant is Black), `allegation` (brief description of the allegation), `fado_type` (type of complaint), and time/date related features (`month_received`, `year_received`, `month_closed`, and `year_closed`). All categorical features except allegation and fado_type were one-hot encoded while the exceptions were ordinal encoded. The numerical features were scaled. 

## Evaluation Metrics
The class imbalance makes accuracy ill-suited for this model, so the F1 score was used instead. The test performance metrics for all groups is as follows:
 - Accuracy Score: 0.623882406425216
 - Recall score: 0.526413921690491
 - Precision score: 0.3299571484222828
 - F1 score: 0.4056513409961685

[(Back to top)](#table-of-contents)

# Overview of Parity Measures and Fairness Results
For a breakdown of different parity measures and fairness in machine learning, take a look at [Google's Machine Learning Glossary: Fairness](https://developers.google.com/machine-learning/glossary/fairness).

With the original model, a singular threshold was used. Under this model, both demographic parity and equalized odds were not satisfied, but predictive value parity was met. The original model substantiated complaints from Black civilians far less often than it did for non-Black complainants. The violation in equalized odds means the model gave more complaints submitted by non-Black complainants the “benefit of the doubt” and classified more CCRB-unsubstantiated complaints as substantiated than for Black complainants.

To try and improve these metrics for fairness, 2 different threshold tests were conducted to find better thresholds based on groups (complainant ethnicity in this case). Firstly, the thresholds that maximize utility for the individual group were used. These thresholds satisfied demographic parity and equalized odds, but not predictive value parity. Secondly, the thresholds that satisfy the 3 parity measures (demographic parity, equalized odds, and predictive value parity) were found using the training data and then tested with a separate dataset. See the paper for a more in depth breakdown on how these tests were conducted.

Depending on what is most important to the decision-making body (CCRB), different threshold(s) would be chosen. Maximizing utility overall enforces equality for all complainants, while maximizing utility for each group is more equitable. Satisfying demographic parity ensures that substantiation doesn’t depend on complainant ethnicity. Equality of odds would focus on ensuring that the chance of obtaining the benefit of substantiation is equal across groups, while predictive value parity focuses on ensuring deserving complainants receive substantiation and underserving complainants don’t. The table below demonstrates different group thresholds that could be used, depending on the goal (maximizing utility or enforcing a parity measure).

|    |   Threshold for Black Complainants |   Threshold for non-Black Complainants | Test                            | Demographic Parity   | Equality of Odds     | Predictive Value Parity   |
|---:|-----------------------------------:|---------------------------------------:|:--------------------------------|:---------------------|:---------------------|:--------------------------|
|  0 |                              0.527 |                                  0.527 | Max utility overall             | Not satisfied        | Not satisfied        | Satisfied                 |
|  1 |                              0.522 |                                  0.546 | Max utility per group           | Satisfied            | Satisfied            | Not satisfied             |
|  2 |                              0.522 |                                  0.541 | Enforce equality of odds        | N/A                  | *Strictly* satisfied | N/A                       |
|  3 |                              0.522 |                                  0.535 | Enforce predictive value parity | N/A                  | N/A                  | Not satisfied             |

[(Back to top)](#table-of-contents)

# Conclusion
Hopefully this paper shows that often times, an algorithm or model may (unintentionally) be unfair or inequitable if such parity measures or metrics of fairness are not considered. As for this specific example of the CCRB, the model missses out on lots of data perhaps gathered in the investigation process, but still demonstrates evidence of inequities or unfairness. The bottom line is that any model or algorithm absolutely should consider its fairness! 

[(Back to top)](#table-of-contents)

