# hw06
## required libraries
```
library(here)
library(tidyverse)
library(readxl)
library(knitr)
library(gridExtra) 
library(knitr)
library(GGally)
library(broom)
```
## Assignment requirement 
For hw06, detailed assignment instruction can be found [here](https://cfss.uchicago.edu/homework/reproducible-research/). 

## My work 
‘Family incidents’ recorded by Victoria Police increased by 6.7 percent from 82,651 in 2018–19 to 88,214 in 2019–20 (a 5% increase in the rate of incidents per 100,000 people), affecting tens of thousands of families across Victoria. As a result, I’d like to use the datasets I’ve acquired to investigate possible causes of domestic violence across Victoria, allowing policymakers to make more informed decisions.
Therefore, my research question is, Do income level and education level have effects on domestic incidence rate? To examine the possible impact of income and education on domestic incidence, I have chosen Victoria state, Australia, as my research setting to conduct the analysis. I wish to find possible correlations between income, education and family violence for policy makers to make more effective policies targeting the issue.

## files introduction
[AURIN_dataset_true.csv](https://github.com/JunyouC/hw06/blob/main/AURIN_dataset_true.csv):
A datasheet from the Australian bureau of statics (ABS) that records the income, education, employability and health statistics by LGA (local government area). For this investigation, we are only interested in certain variables including (for a person over the age of 15): completed school years and the weekly total personal income for residence in victoria, Australia. The data are collected by the ABS from the 2016 census of Population and Housing.

[V_Police_Data_2012-17.xlsx](https://github.com/JunyouC/hw06/blob/main/V_Police_Data_2012-17.xlsx):
Bureau of crime statistics data sheet on victims of domestic violence recorded by Victorian police.This includes data recorded between July 2012 and July 2017, and 21 data sheets on many different aspects of domestic violence cases reported to the police, including the gender and age of affected members, children’s participation in domestic violence cases, etc. However, the main data of this study are **Table 2** and **Table 3**.
In my analysis, **Table 2** has been stored as family_incidence, including family event data recorded in police areas and local government areas from July 2012 to June 2017. **Table 3** has been stored as family_incidence_rate, including the data of household accident rate per 100000 population divided by police district and local government area from July 2012 to June 2017.
[domestic violence analysis.Rmd](https://github.com/JunyouC/hw06/blob/main/domestic%20violence%20analysis.Rmd):
This Rmarkdown file contained the raw code I've used to do the analysis. 
[domestic-violence-analysis.md](https://github.com/JunyouC/hw06/blob/main/domestic-violence-analysis.md):
I'd like to call this rendered mardown file as my report.version file for my analysis as I have hide all code parts so as to not to confuse whoever is reading it. 

## Thoughts 
This assignment is challenging in sense that it does not explicitly asking us what to do but leave it all to us to decide. 
The data I've chosen is from another Python class. I tried to redo some parts of it using r instead of Python and also added some new analysis to make it more holistic.
There are 3 challenges I've encountered that I found especially hard:
- The original region_name column in AURIN_dataset_true.csv is not identical with the ones recorded in V_Police_Data_2012-17.xlsx. Every value has 4 more letters in the tail (ex. (C),(B),(C)...) following its original name. I first came up with a solution that would help me select the first word of every value. I thought it worked until I found that there are some names aren't consisted of just one word! (ex. yarra renges... ) Therefore I was forced to figure out another way that would permit me to just delete the last 4 letters. 
- It took me quite some time to figure out how to lay out the summary table that join all needed information. For the summarizing table, I first used `pivot_long()` to created columns for income and education_level, but soon I found that in doing so, there would so many duplicates that could produce some unexpected errors. What's more, the column `region_name` would no longer be the primary key. For a data that lacks primary key, it is hard to do analysis efficiently. 
- Since for most of my plots the x-axis is consisted of 79 regions in State of Victoria (that's a lot!), when I first try to knit it, I found that all words are overlapsed and can hardly be read. I first try to change the size of the picture by setting default in the yaml header, but I soon found that it was not the fault of the size of the picture that made it so unreadable but the size of the letter. Therefore, I later modified word size for some of my plots and now it looked so much better!


