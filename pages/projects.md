---
layout: page
title: Final Projects
---

Students will work in small groups of 3-4 students on a month-long data science project. The goal of the project is to go through the complete data science process to answer questions you have about an assigned dataset and prompt. Canvas or Slack can be used to find prospective team members. In general, we do not anticipate that the grades for each group member will be different. However, we reserve the right to assign different grades to each group member based on peer assessments (see below).

Each group must complete and submit [this project preference form](https://docs.google.com/forms/d/e/1FAIpQLSd5ankpYNTgtTjWJsRAatK0rGHqnPKfAVTRMDubv_7j29enew/viewform?usp=sharing) **by 11:59 pm EST on November 7, 2022**. We will take preferences into account when assigning each group a project.


## Project Prompt
You and your team of data scientists were hired by a company to gain insights on the dataset in your assigned prompt. 

1. Perform any necessary data pre-processing and cleaning, and document your steps. Depending on the prompt you are assigned, this may involve transforming variables, creating new variables, and merging data frames. In particular, you may need to make some decisions on how to handle missing data, such as removing rows or columns with a significant amount of missing observations, creating an "unknown" category, or replacing/imputing the missing values. You do not need to develop a rigorous process or cite references, but please briefly justify your choices. 

2. Make and interpret 4-10 visualizations to help you understand the relationships between the variables in your dataset. We highly encourage you to explore the data on your own, but when preparing your response to this question, please be parsimonious in your plots and select visualizations that help you tell a story about the data. If you need to make additional plots to support your responses to the other questions (e.g. to motivate data cleaning or modeling choices), that's fine. 

3. Build any 2 machine learning models that use your choice of covariates to predict the given outcome variable. Explain why you chose those covariates and interpret the models. If you are including categorical variables as covariates in a `glmnet` model (lasso or ridge regression), please remember that you will need to convert your covariate data frame into a *model matrix*, e.g. by calling the `model.matrix` function:

```r
model_matrix = model.matrix(~.-1, my_covariate_df)
```

4. The company stakeholders want to know what decision they should make on their stated goal/question. Based on your analysis, make recommendations for a non-technical audience. 

5. Is there any additional information or data that might be useful to collect/have for answering your prompt?


## Project Options
### Obstetrics and periodontal therapy 

The `opt` data frame in the `opt.rData` file contains data from a randomized controlled trial that was used to determine whether treatment of maternal periodontal disease can reduce risk of preterm birth and low birth weight. This dataset was taken from the [`medicaldata` R package](https://github.com/higgi13425/medicaldata); documentation can be found [here](https://higgi13425.github.io/medicaldata/reference/opt.html). Your goal is to assess if maternal periodontal disease treatment impacts birthweight and determine whether treatment should be recommended moving forward. 

During the data processing step, you will need to create a low birthweight variable, where low birthweight is defined as <2500 g. This is the outcome variable that you should use in your models. Please note that several numeric variables were coded as factors in this dataset (see documentation or explore this on your own), but you most likely do not want to treat them as factors/categorical. 


### NHANES (2013-2014)

The National Health and Nutrition Examination Survey (NHANES) assesses the health and nutritional status of adults and children in the United States. The `covariate_df` data frame in the `covariate_df.rData` file contains the demographic, examination, diet, and lab data from [NHANES 2013-2014](https://www.kaggle.com/datasets/cdc/national-health-and-nutrition-examination-survey). You can peruse the dictionaries for the variables on the CDC website: [demographics](https://wwwn.cdc.gov/Nchs/Nhanes/Search/variablelist.aspx?Component=Demographics&CycleBeginYear=2013), 
[examinations](https://wwwn.cdc.gov/Nchs/Nhanes/Search/variablelist.aspx?Component=Examination&CycleBeginYear=2013), 
[diet](https://wwwn.cdc.gov/Nchs/Nhanes/Search/variablelist.aspx?Component=Dietary&CycleBeginYear=2013), and
[lab](https://wwwn.cdc.gov/Nchs/Nhanes/Search/variablelist.aspx?Component=Laboratory&CycleBeginYear=2013). Your goal is to use these covariates to predict the occurrence of diabetes, cancer, heart attack, stroke, OR depression. The company wants you to recommend a predictive model and identify key variables that appear to associated with the outcome disease. 

As part of data processing, choose ONE of the five diseases and merge the corresponding variable from the `questionnaire.csv` dataset with `covariate_df`. This disease is the outcome that your model should predict. The relevant variable names in `questionnaire.csv` are: DIQ010 (diabetes), MCQ220 (cancer), MCQ160E (heart attack), MCQ160F (stroke), and DPQ020 (depression). (You can view the entire questionnaire dictionary [here](https://wwwn.cdc.gov/Nchs/Nhanes/Search/variablelist.aspx?Component=Questionnaire&CycleBeginYear=2013).) For each disease variable, you can take `1` to be affected, `2` to be unaffected, and all other numeric values to be unknown/ignored. 


### NYPD complaints

`allegations_202007271729.csv` contains records about closed cases for every police officer on the NYPD force as of late June 2020 who had at least one substantiated allegation against them, spanning from September 1985 to January 2020. Information on the variables in this dataset can be found in `CCRB Data Layout Table.xlsx`. This data was downloaded from 
[Kaggle](https://www.kaggle.com/datasets/mrmorj/civilian-complaints-against-nyc-police-officers) and originally reported on by ProPublica. Your goal is recommend a model to predict the disposition ruled by the Civilian Complaint Review Board (CCRB) and identify key variables that appear to be associated with the board's ruling. 

Please restrict your analysis to observations that were either "Substantiated" or "Exonerated", excluding observations that were "Unsubstantiated". This means that your models should predict whether the CCRB determined that the officer violated NYPD rules (yes = Substantiated, no = Exonerated), excluding cases where the CCRB could not conclude if the conduct occurred (Unsubstantiated). If you choose to incorporate information on officer rank and command, you will most likely want to collapse or otherwise simplify the categories for these variables (see the Rank Abbrevs and Command Abbrevs tabs in `CCRB Data Layout Table.xlsx`). If you do so, please briefly justify your reasoning. 


### Project Milestones
There are a few milestones for the final project. **It is critical to note that no extensions will be given for any of the project due dates for any reason, except for COVID-19 related emergencies or other unforeseen emergencies. Late days may not be used.** Projects submitted after the final due date will not be graded. Students who anticipate any issues should send an email to the teaching staff at least one week in advance.


| Date       | Description |
| ------------- |-------------|
| November 7 by 11:59pm EST| Form a team and submit the project preference sheet|
| November 7 - 18| Project review meeting with your assigned TF |
| December 12 by 11:59pm EST| RMarkdown and compiled HTML due |
| December 12 by 11:59pm EST| Peer assessment due |


## Deliverables
There are several deliverables for your project that will be graded individually to make up your final project score.

### Team Registration and Preferences
Each group must complete and submit [this project preference form](https://docs.google.com/forms/d/e/1FAIpQLSd5ankpYNTgtTjWJsRAatK0rGHqnPKfAVTRMDubv_7j29enew/viewform?usp=sharing) **by 11:59 pm EST on November 7, 2022**. We will take preferences into account when assigning each group a project. Each group only needs to submit 1 form. A teaching fellow will be assigned to each team and will help guide students through the project. Students will schedule a project review meeting with their assigned TF within the following two weeks (November 7-18, 2021). Students should ensure all of your team members are present at the meeting.


### RMarkdown and HTML Files
An important part of the project is the RMarkdown and associated HTML file. These will detail the steps taken in answering each of the project prompt questions. Equally important to the final results is how the team got there! The RMarkdown and HTML files are the place you describe and document the space of possibilities explored at each step of the project. The RMarkdown and HTML files are due Monday, December 12 by 11:59pm EST. Your assigned TF will create a repository for you to submit your project files.


### Code
We expect you to write high-quality and readable R code in your RMarkdown file. You should strive for doing things the right way and think about aspects such as reproducibility, efficiency, cleaning data, etc. **We also expect you to document your code.**

### Peer Assessment
It is important to provide positive feedback to people who truly worked hard for the good of the team and to also make suggestions to those you perceived not to be working as effectively on team tasks. We ask you to provide an honest assessment of the contributions of the members of your team, including yourself. The feedback you provide should reflect your judgment of each team member:

* **Preparation**: were they prepared during team meetings?

* **Contribution**: did they contribute productively to the team discussion and work?

* **Respect for others’ ideas**: did they encourage others to contribute their ideas?

* **Flexibility**: were they flexible when disagreements occurred?

Your teammates' assessment of your contributions and the accuracy of your self-assessment will be considered as part of your overall project score. The peer assessment is due Sunday, December 12 by 11:59pm EST. For instructions on how to submit, please see **Submission Instructions** below. 


#### How to submit the Peer Assessment (due Monday, December 12 by 11:59pm EST)
Each individual team member needs to fill out this [google form for the peer evaluation](https://docs.google.com/forms/d/e/1FAIpQLScQaOxM9WOt0bsO3vWA2vy26yHvkUtOzy5gby5alU3Rj33HHA/viewform?usp=sharing). Your individual project score will take into account your self and peer assessment. 


## Grading
The final project is graded in two parts:

1. Final Project Part I (worth 10% of total grade). This portion represents the Team Registration and Project Preferences which is due November 7 by 11:59pm EST.

2. Final Project Part II (worth 25% of total grade). This portion will be based on your RMarkdown and HTML files in your GitHub repository. This includes the quality of your data analysis and R code, completeness and overall functionality of your analysis. This portion (and peer assessment) is due Monday, December 12 by 11:59pm EST.

Your individual project score will also be determined by your peer evaluations.

