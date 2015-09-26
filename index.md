---
title       : Cardiovascular heart disease prediction
subtitle    : 
author      : J. Faxas
job         : 
framework   : io2012       # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Cardiovascular heart disease prediction.

A Cardiovascular heart disease (CHD) predictor has been developed for the Developing Data Products course. It predicts whether a person is at risk of contracting cardiovascular disease in the next 10 years.

The logistic regression model was generated with data from the Framingham Heart Study, a long term prospective study of the etiology of cardiovascular
disease among a population of free living subjects in the community of Framingham, Massachusetts.

--- .class #id 

## Building the model

To generated the regression model with the data we use the following code:


```r
framinghamLog<-glm(TenYearCHD~male+age+cigsPerDay+totChol+
                     sysBP+glucose,data=train,family = "binomial")
```
Where TenYearCHD is the 10-year CHD prediction, male a binary variable that represents if the person is male or female, the age in years, cigsPerDay is the number of cigarettes smoked each day,totChol is Serum Total Cholesterol in mg/dL, sysBP is the Systolic Blood Pressure in mmHg and glucose is Casual serum glucose (mg/dL).

--- .class #id 

## Final model

The final model looks like this:

```r
HeartDiseaseRisk<-function(gender,age,cigsPerDay,totChol,sysBP,glucose){
  Logy<- -9.496692+0.440083*gender+0.066553*age+0.020706*cigsPerDay+
    0.002897*totChol+0.018244*sysBP+0.009031*glucose
  y<-exp(Logy)
  isRisk<- y>0.5
  if (isRisk==1) {
    print("You are UNDER RISK to develop a coronary heart disease in the next 10 years")} 
    else 
      {print("You have LOW RISK to develope a coronary heart disease in the next 10 years")}
  
 
}
```

--- .class #id 

## Test the model

In order to test the model, some values will submmit to the function. Then, a sentence with the prediction will be printed.

```r
  gender=1 #male
  age= 30
  cigsPerDay=20
  totChol=250 # mg/dL
  sysBP=120 # mmHG
  glucose=150 # mg/dL
  
  HeartDiseaseRisk(gender,age,cigsPerDay,totChol,sysBP,glucose)
```

```
## [1] "You have LOW RISK to develope a coronary heart disease in the next 10 years"
```
  
