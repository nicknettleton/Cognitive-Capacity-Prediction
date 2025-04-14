# Introduction

For my portfolio project, I work with a dataset from the from Mexican Health & Aging Study, https://www.mhasweb.org/. The objective is, using social determinants such as education, lifestyle, work and family, to predict individuals' cognitive capacity 6-18 years into the future, as a risk indicator for Alzheimer's and related dementias, so that health services can be targeted to where they are needed most.

I find that it is possible to predict with a surprising degree of accuracy given this data alone. I find that societal factors, such as education, and lifestyle factors, such as whether an individual has an active social life, play an outsize role in long term dementia outcomes. This is significant, because it 

I have been working on this model throughout the course, initially as part of a major international competition organised by the US National Institutes for Health (https://www.nih.gov/). I came second worldwide out of 400 entrants in the Model Arena, for predictive accuracy (https://www.drivendata.org/competitions/300/competition-nih-alzheimers-sdoh-2/), and also won an Explainability Bonus prize in the Reporting Arena (https://www.drivendata.org/competitions/301/prepare-challenge-phase-2-report-arena/page/939/). My final submission can be found here: https://github.com/nicknettleton/PREPARE-Challenge. I'm really proud of this achievement given that I only started learning in September last year!

I have continued to update and improve my model during the course, to test and practice many of the techniques learned.

### About the data

Although the study is limited to Mexican individuals, it forms part of the global Gateway to Global Aging Data project (https://g2aging.org/home) where harmonised data is available. This means that in principle, learnings from it can be adapted and trained to help with long term health prediction for individuals all over the world.

The specific data I have used come from the MHAS Core survey Data 2003 and 2021 (https://www.mhasweb.org/DataProducts/CoreSurveyData.aspx) and Ancillary Studies 2016 and 2021 (https://www.mhasweb.org/DataProducts/AncillaryStudies.aspx).

This data is longitudinal and consists of:

1. Two surveys carried out on Mexican individuals aged 40+, in 2003 and 2021, into their lifestyle and social determinants
2. Two cognitive assessments carried out in 2016 and 2021

The features consist of [todo].

The target variable is cognitive score, which is measured on a range of todo.

Not all individuals completed both surveys or assessments, so there are many gaps in the data, as we would expect for a study of this type. Part of the objective of the model is to navigate this noise.

### About the model

**Overall strategy and metrics**

Cognitive score is an integer between 0 and [todo]. Thus this is a regression problem. RMSE is the primary metric. todo - any others? (fairness in regression metric?)

The data is split into training-validation and test sets. I experiment, evaluate and and compare many modelling using cross-validation on the training-validation set. The test is treated as wholly unseen data, i.e. it is used only for final benchmarking of model performance.

**Data preparation**

The data can be organised in four different ways: long (one row per survey per cognitive assessment), wide (one row per unique individual), or a hybrid format. I find the best results are achieved by organising the data with one row per cognitive assessment. This means that individuals who had two assessments will have two rows in the data, and therefore to ensure generalisability, group cross validation is needed to data leakage.

Todo: more here

EDA

**Imbalance**

Cognitive capacity is distributed (close to) normally in the population, and in the training data. This means that there are many less samples of individuals with very low or very high cognitive scores. This rarity makes it harder to make accurate predictions for these groups, but we are particularly interested in being able to predict very low scores so early intervention can be planned. To help with this, I explore a number of different measures to address the imbalance, including oversampling, undersampling, sample weighting and SMOTER/SMOGN.

Pre-processing

Feature engineering

**Cognitive prediction**

I evaluate a large numer of different algorithms against the data using cross-validation to provide a robust estimate of predictive performance and generalizability. Todo: I find that...

**Bayesian Optimisation**

I use Bayesian Optimisation to tune and select the best ``n`` models for a final ensemble and their weightings within it.

**Prediction intervals**

**Fairness**

Fairness are crucial in health. Although the data does not include features such as ethnicity, it does include gender. I evaluate the model for fairness. 

**Final evaluation**

I evaluate predictive performance using cross validate, and provide a final benchmark of model performance by measuring error on the test set.

**Explainability**
Finally, ...