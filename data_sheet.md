# Datasheet: Predicting Future Cognitive Capacity

Datasheet version: v0.1

Date the datasheet was created/updated: 14 April 2025

Contact information for questions: Nick Nettleton, https://github.com/nicknettleton

---

The data for this model comes from the Mexican Health & Aging Study, https://www.mhasweb.org/, which has been running from 2001 to the present data.

The specific datasets used are:

1. 2016 and 2021 Cognitive Aging Ancillary Studies (Mex-Cog), Cognitive Assessment STATA files. These can be downloaded from https://www.mhasweb.org/DataProducts/AncillaryStudies.aspx.

2. The 2001, 2003 and 2012 Constructed Data, Created Variables STATA files. These can be downloaded from https://www.mhasweb.org/DataProducts/ConstructedData.aspx.

Although focused on Mexican individuals, the project is linked to the [Gateway to Global Aging Data project](https://g2aging.org/), which aims to provide harmonised global datasets. So I anticipate the techniques developed here might be applied globally.

## Motivation

The Mexican Health & Aging Study (MHAS) is a national longitudinal study of adults 50 years and older in Mexico. The baseline survey, with national and urban/rural representation of adults born in 1951 or earlier, was conducted in 2001 with follow-up interviews in 2003, 2012, 2015, 2018, 2021 and 2024.

The objective of the study is to provide data for research and insight into healthy aging.

The study is a collaborative effort among researchers from the University of Texas Medical Branch (UTMB), the Instituto Nacional de Estadística y Geografía (INEGI, Mexico), the Instituto Nacional de Geriatría (INGER, Mexico), the Instituto Nacional de Salud Pública (INSP, Mexico), Columbia University, and University of California Los Angeles (UCLA).

The MHAS (Mexican Health and Aging Study) is partly sponsored by the National Institutes of Health/National Institute on Aging (grant number NIH R01AG018016) in the United States and the Instituto Nacional de Estadística y Geografía (INEGI) in Mexico. The MHAS Cognitive Aging Ancillary Study Waves 1 and 2 (Mex-Cog 2016 and 2021) were sponsored by the National Institutes of Health/National Institute on Aging (NIH R01AG051158/R56AG059756).

The concept for the subset of data used for this model comes from a subset created for the [DrivenData PREPARE Challenge](https://www.drivendata.org/competitions/group/nih-nia-alzheimers-adrd-competition/). However, I have reverted to the original source, which has greater depth, and included additional data in the model.

## Composition

The instances in the model data represent 9368 surveys (in 2001, 2003 and 2012),and 5325 cognitive assessments (in 2016 and 2021) carried out for 4001 unique individuals. Key social determinant features derived from these surveys include variables related to demographics (such as age, gender), socioeconomic status (such as education level, income indicators, employment status), location (such as urban/rural), social factors (such as marital status, living arrangements), and lifestyle (such as hobbies, interests, activities).

All individuals in the model data used completed at least one survey and one cognitive assessment. There are many gaps in the data where individuals did nto complete all three surveys or both cognitive assessments.

The data is anonymised for research purposes, but nevertheless includes confidential health data.

## Bias

The underlying study was designed to be reflective of the Mexican population for people aged 50+.

However, in the data used for this model, there are some individuals aged below 50, and by the nature of the population distribution, many less in the data aged over 70 and over 80.

Cognitivity capacity, which is measured by composite_score, is distributed near-normally with a mean of 159. The lowest possible is 0, and the highest possible is 384, where higher is better. This distribution means that there are far fewer samples for those with very low and very high scores than those around the mean, which impacts our ability to make accurate preditions for those individuals. This makes it challenging to accurately identify those with the highest risk early based on social determinants alone - something which may need addressing for models that need to deliver high sensitivity or balanced performance, for example.

Although the study was designed to be reflective of the Mexican population, in the data I have used there are roughly 44% more samples for females than males, which introduces a risk of unfair analysis based on gender. 

The notebook includes a more detailed analysis of these and other key protected characteristics and social determinants.

This data does not include information about ethnicity or sexual orientation, which would be helpful to identify any potential bias in these important protected characteristics.

## Collection process

The data used for the model was collected in study waves between 2001 and 2021 through interviews and assessments directly with individuals and next of kin.

Full details of the methodology can be found at https://www.mhasweb.org/Documentation/Home.aspx.

## Preprocessing/cleaning/labelling

Extensive preprocessing, cleaning and labelling has been carried out by the MHAS on the original raw data, details of which are documented alongside the respective file downloads, linked above.

This models uses as raw data the data provided by MHAS. The data across the different dataset is merged on Unique Household ID and Person ID. Samples are removed where there is either no survey or no cognitive assessment for an individual.

The cognitive capacity label used, composite_score, is calculated from the underlying cognitive assessment data following the methodology set out for the PREPARE Challenge at https://www.drivendata.org/competitions/300/competition-nih-alzheimers-sdoh-2/page/930/:

    Composite score is the number of points that an individual received across seven domains:

    Domain	                Example task or question    	Possible score
    Orientation	            Where are we now?	            9
    Immediate memory	    Word repetition tests	        95
    Delayed memory	        Delayed recall of a short story	106
    Attention	            Ability to count backwards	    65
    Language	            Write a sentence	            14
    Constructional praxis	Physically copy a drawn figure	12
    Exective function	    Simple math question	        83

Experiments have been carried out with discretization and processing missing values, but these are not used in the final model. Therefore, in the pipeline feeding the final model, categorical features and missing values present in the prepared MHAS data are handled directly by the model architecture.
 
## Uses

The objective of my model is to assess how effectively we can predict future cognitive capacity based on social determinants, as a risk indicator for Alzheimer's disease and Alzheimer's disease related dementias (AD/ADRD), so that health services can be efficiently targeted to where they are needed most.

The underlying MHAS data used is a rich resource for study of health, social determinants and aging, and has been the subject of the large number of research publications - see https://www.mhasweb.org/Publications/Home.aspx.

From an AI perspective, it could be used in many ways to explore complex, evolving patterns of health, social determinants and aging, and potentially to forecast future trends too. Through the harmonized data shared by the Gateway to Global Aging Data project, data might be aggregated globally to build a richer and more comprehensive dataset for prediction and also to compare health based on geographical and societal factors.

From an ethical perspective, part of the purpose of social determinants data is to understand the interplay of societal factors and health equity, and improve health equity for those who need it most. This topic is covered in depth by the WHO at https://www.who.int/health-topics/social-determinants-of-health. However, all data contains bias. I have detailed above some key areas of bias that I have identified in the data, which need to be borne in mind when using it.

It is important to note that this is not a clinical dataset. It does not factor in medical data. It is perfectly possible to have social determinants predictive of a certain cognitive capacity, while actually having something very different. Intuitively, this makes sense, and is in fact a desirable objective: in an ideal world, non-medical factors would have little to no influence on our health.

## Distribution

The data is distributed by MHAS via https://www.mhasweb.org, and is subject to the copyright, intellectual property (IP) license, confidentiality and other terms of use documented on that website. In particular (as at 14 April 2025):

• User will not attempt to identify subjects/study participants.
• User will not distribute his/her MHAS username and password.
• User will not transfer MHAS public release data to a third party(-ies), with the exception of staff or students for whom said user is directly responsible.
• User must properly credit MHAS for the use of any data and the link to the public data must be included.

## Maintenance

The data is maintained by MHAS.