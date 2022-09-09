# Algorithmic Audit: Analyzing the Fairness and Potential Inequities in the Review of Civilian Complaints to the NYPD

![banner](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/e6fe2eb9f6dbe7af249f0bac74fd1296b2e5d088/Screen%20Shot%202022-09-08%20at%205.37.33%20PM.png)

[CCRB logo](https://www1.nyc.gov/assets/ccrb/images/content/pages/board-members/image_missing.png), [NYPD logo](https://en.wikipedia.org/wiki/New_York_City_Police_Department)

## [For Full Paper, Click Here](https://github.com/jacquelinekclee/algorithmic-audit-nyc-ccrb/blob/aa536a7c4a71f71eaf114cd817be665e8a0b5252/paper2.pdf)
Please note that this README functions only as an overview of the work done!

# Table of contents

- [Background](#background)
- [Tools Used](#tools-used)
- [The Data](#the-data)
- [The Logistic Regression Model](#the-logistic-regression-model)
- [Overview of Parity Measures and Fairness](#overview-of-parity-measures-and-fairness)
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

The data originally comes from [ProPublica](https://www.propublica.org/datastore/dataset/civilian-complaints-against-new-york-city-police-officers)

[(Back to top)](#table-of-contents)

# The Logistic Regression Model

[(Back to top)](#table-of-contents)

# Overview of Parity Measures and Fairness

[(Back to top)](#table-of-contents)

# Findings and Conclusion

[(Back to top)](#table-of-contents)

