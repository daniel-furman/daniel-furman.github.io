---
title: "Field experiment on dating attitudes towards academic prestige"
date: 2022-05-09
katex: true
markup: "mmark"
---

# Field experiment on dating attitudes towards academic prestige in the Bay Area.

### By Daniel Furman, Forrest Brandt, and Jackie Hu

* Berkeley Spring 2022, Causal Inference with Prof. Josue Martinez

---

## Objective

How significant is one’s academic prestige for online dating in the Bay Area? Are dating attitudes towards academic achievements different between men and women in the Bay Area? 

The widespread adoption of online dating apps enables social scientists to perform field experiments probing the underlying psychology of human dating, for example, how social attractiveness influences dating dynamics. Here, we define social attractiveness as elements of one’s personality other than physical attractiveness that play into human dating, for example, academic and career achievements, socio-economic class, hobbies, intelligence, etc. The intervention of our experiment is the modification of academic history within otherwise identical dating profiles on online dating apps (Tinder) for heterosexual profiles, with the treatment being a highly selective university (Princeton) and the control being a lower-tiered university (Rutgers). Our results suggest that academic prestige is significant for online dating pools in the Bay Area, as we observed that Princeton gave a boost in matching rates compared to Rutgers profiles across both genders (ATE = 19% with a confidence interval from 10.6% - 26.8%, SE of 4%). Second, we found that women are more likely to act on social attractiveness when selecting matches on online dating apps compared to men, with Princeton giving a threefold boost compared to Rutgers for women matching with men, which is in stark contrast to the twofold boost for men matching with women.

## Treatment Design

To investigate how social desirability differs between men and women we performed simple field experiments on Tinder.

* Profile 1: Went to Princeton, male (Treatment)
* Profile 2: Went to Rutgers, male (Control)
* Profile 3: Went to Princeton, female (Treatment)
* Profile 4: Went to Rutgers, female (Control)

To reduce the influence of the matching hypothesis on whether or not someone swipes “match” on our profiles, we selected colleges that should have roughly equal representation in the Bay Area. If our recruits were only selecting “match” because the profiles share an alma mater, then the conversion rate would perhaps not be measuring the underlying mechanisms of interest. Princeton University and Rutgers University are two East Coast schools where we believe the population overlap between alumni and Bay Area residents are relatively minimal.

## Experiment Design

First, we created 4 Tinder profiles varying in the dimensions identified in the treatment variants section. We configured the sexual orientation of the profiles to be heterosexual and to search for matches between ages 21-30 within a 50-mile radius. For each of the different profile variants, the members of the research group swiped “match” for 100+ unduplicated profiles and recorded metadata for each swipe, such as name, age, whether include work or school information. Doing so at roughly the same time and the same location for all profile variants was aimed at reducing the number of confounding factors influencing our experiment.

## Measurement design

We gathered data on the outcome variable (likelihood to match), collecting the profiles that we interact with when swiping “right”, such as name, age, dummy variables for college info, and work info listed in their profile. Gathering this data allowed us to see if there are heterogeneous effects within the population.

We then removed all of the profiles from the sample that appeared for both the treatment and control, since seeing two similar profiles would be suspicious and most likely affect the individual’s decision to swipe “right” or “left”. We measured the difference in means of the conversion rates between the treatment and control groups while assessing if there were heterogeneous effects within the population.

## Pilot

We ran a pilot a week before the actual experiment and recorded measurements as planned. The pilot suggested that we were more likely to swipe on the same batch of profiles if the treatment and control profiles were swiping at the same time and location, which results in contamination and duplicated data in the final results. In the actual experiment, we decided to extend the experiment to a week instead of a few days and expanded the location from solely Berkeley to the entire Bay Area (mainly San Francisco, Berkeley, and Emeryville). These steps helped to avoid swiping on the same batch of profiles. The adjustment still conforms to our experimental design and is valid for testing our hypothesis. We successfully collected data on at least 100 unique profiles for both control and treatment for each gender, with the final count at 413 valid observations.

## Covariates

The covariates we chose to collect for our linear model are:
* Age
* School - whether a profile has information about the school that person attended 
* Work - whether a profile has information about the person’s place or work

These variables were found in the profile’s metadata. We discussed including other variables such as ethnicity, but Tinder does not include that information and a subjective guess on our part could be problematic and misrepresent users; therefore, we decided not to include that information. We also discussed extracting certain information from the user’s bio since it is a free-form text entry. However, during the pilot, we found high variation within the free-form text entry. Some profiles had extensive information, some non-relevant information, and others chose to leave that field blank. In the end we decided not to extract information from the bio and stayed with the four variables listed above.

## Randomization

Our population of interest are all heterosexual dating profiles on Tinder within a 50-mile radius of the Bay Area aged 21-30. The sample of profiles we interact with does not come from a random sample of all Bay Area profiles on Tinder. Our experiment relies on Tinder selecting profiles to show us and show our profile to prospective matches, given our filter preference. While conducting our experiment, if any profile appeared for both profiles, we excluded that profile from both datasets, since the decision for that user to swipe right or left on our profile could be influenced by seeing two of the exact profiles, with only the school changed. Because our experiment is not fully randomized, it is imperative to conduct a covariate balance check to ensure an even distribution within our sample.

## Covariate Balance Checks

There are two ways to check for covariate balance to see if our randomization worked. The first is to conduct a t-test for the difference in means for each of the covariates split on the treatment variable. However, this method is subject to the possibility of falsely rejecting the null hypothesis at higher rates than our critical value. Instead we choose the second method proposed by Gerber and Green, which is to run an F-test to compare a model with no predictive features and a model that explains random features. The summary of the F-test is below:

```
Analysis of Variance Table
Model 1: Treatment ~ Age + School + Work
Model 2: Treatment ~ 1
  Res.Df    RSS Df Sum of Sq      F Pr(>F)
1    432 107.49
2    435 108.96 -3   -1.4739 1.9745 0.1171
```

As the table shows, the F-statistic is less than two and the p-value is greater than 0.05, our chosen alpha level. This indicates there is not a difference between the two models since we fail to reject the null hypothesis, and the sample passes the randomization check.

## Results

Our hypothesis regarding our first research question was that Princeton improves matching rates compared to Rutgers. The results of the field experiment reveal that Princeton profiles (83/211, 39%) indeed were significantly more likely to match than Rutgers profiles (37/203, 18%), with a corresponding ATE of 19% (SE=0.04, p-value=1e-6). In addition, both Welch’s T-Test and Permutation tests on the mean revealed a p-value of less than 1e-13. And, lastly, the Cohen's practical significance test showed that the effect size is medium (d=0.41). The 97.5% confidence interval for treatment is between 0.106 and 0.268. 

Our hypothesis regarding our second research question was that women are more likely to act on academic prestige when selecting matches compared to men. The results reveal that females (Princeton 19/114, 17%; Rutgers 6/107, 6%) were significantly more likely to act on academic accomplishments than men (Princeton 58/97, 60%; Rutgers 31/95, 33%). Both Welch’s T-Test and Permutation tests on the percentage decrease between Princeton and Rutgers revealed a p-value of less than 1e-13. Bootstrap resampling was employed to obtain a thousand different estimates of the percentage decrease per gender, which were used for the aforementioned difference in mean tests. And, lastly, the Cohen's practical significance test showed that the effect size is very strong (d=1.51). However, these results should be taken with a grain of salt, because the larger Rutgers match rate for women profiles made it nearly impossible to compare the two genders as we intended. For example, to match the over threefold increase observed for women matching male profiles, the female profiles would have needed to obtain a matching rate of over 100%, a significant limitation of our study that in some ways invalidates these results regarding the second research question.

## Excludability & Generalizability
Consistent with previous literature on the topic, our results show that participants are more likely to swipe (show interest) on potential partners if that person attended a more prestigious school. The effect was strong for both male and female populations but was stronger for females swiping on male profiles. We believe this experiment does generalize beyond the Bay Area, primarily due to the effect size and small standard errors. However, we would recommend subsequent experiments to confirm these results. The Bay Area is known as a highly competitive area that brings in talented individuals for high paying jobs. The Bay Area population is skewed towards higher income, more educated workforce that would most likely affect our results. It would be understandable if our ATE is overestimated due to the population we sampled. This experiment should be conducted in other regions around the country to have a more robust understanding of this question.

## Limitation and Future Work

### Noncompliance and Attrition
Our experiment is not concerned with noncompliance and attrition since we are simply measuring the match rate of our profiles. In regards to noncompliance, it could be the case that users who we swiped right on never see our profile due to Tinder not selecting us as an option. In this scenario, the user never receives the treatment. To mitigate this issue, we looked at match rates over a 7-day period to help ensure our profile is shown to all users we interacted with. While we cannot guarantee our profile is shown to all users, we believe a 7-day period is sufficient to decrease the odds of that issue happening. We are also not concerned with attrition since a user we see would have to leave Tinder within the 7-days we run our experiment. It could happen that we swipe right on a user then that user deletes their profile prior to seeing ours, but we believe this scenario is unlikely to happen very often for it to be a concern.

### Spillover
Generally, we were not concerned with spillover effects in our experiment since it is unlikely that the profiles our treatment and control are interacting with would be communicating with other profiles. However, it could be the case that multiple people within a friend group could be on Tinder and discuss or compare the various profiles they see. One person could see the control or treatment and show the profile to a friend who might come across our profile at a later time. If the interaction with previously seeing the profile from a friend influences that person’s decision whether to swipe right or left, it would affect our ATE. We could see both cases for positive or negative spillover effects which would underestimate or overestimate the ATE, respectively. Due to the small chance of this scenario occurring, we are not concerned with spillover effects.









