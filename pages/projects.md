---
layout: page
title: Final Projects
---

Students will work in small groups of 3-4 students on a month-long data science project. The goal of the project is for the participants to practice and apply the machine learning models and techniques taught during the two weeks on real health data. 
In general, we do not anticipate that the grades for each group member will be different. However, we reserve the right to assign different grades to each group member based on peer assessments (see below). This project would serve as prerequest for the Deep Learning Short Course that will be organised in June/July, 2023.


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

