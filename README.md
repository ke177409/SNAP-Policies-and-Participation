# SNAP Policies and Participation: Project Overview
### [Tableau Dashboard](https://public.tableau.com/app/profile/kara.evans/viz/SNAPPoliciesParticipation/SNAPPoliciesParticipation?publish=yes)

The Supplemental Nutrition Assistance Program (SNAP) is a federally funded initiative collaborating with states to provide monthly food benefits to low-income individuals and households. Following welfare reform legislation in 1996, states gained greater autonomy in administering SNAP, leading to variances in state programs. This analysis aims to spotlight the evolution of policies in states with elevated participation rates. As states adopt more accommodating policies for recipients, SNAP participation rates are likely to increase.
<p align="center">
<img src="Images/corr_heatmap_3.png" width=700 height=660>
</p>
A correlation heatmap was constructed using the Seaborn heatmap function in Python to reveal the influence of policies on one another. Five policies displayed significant correlations with each other:

* **Broad-Based Categorical Eligibility** (BBCE) allows states to increase income and asset eligibility limits for low-income households. BBCE demonstrated a moderate positive correlation (0.59) with policies that refrain from limiting the **number of household vehicles**, which are considered assets.
* Policies that do not impose restrictions on household vehicles and policies that offer the **simplified reporting option** had a slightly stronger correlation (0.61). Simplified reporting reduces the requirements for households to report changes in their circumstances.
* Policies that allow **telephone interviews** (instead of face-to-face interviews) during initial certification had a moderate positive correlation with policies that allow households to **apply for SNAP online** (0.59). 

<p align="center">
<img src="Images/regression_train.png" width=500 height=460>
</p>

I hypothesized that as proportions of individuals with earned income increases, proportions of nonearning individuals will also increase. To test this hypothesis, a linear regression analysis was conducted to examine how variations in the proportion of earners impact the proportions of nonearners. A strong positive linear correlation of 0.89 was identified between these groups, particularly among those subject to 7-to-12 month recertification periods. The model had a mean squared error of 0.0339 and an R2 score of 0.7973 for the training set. These statistics indicate that the model exhibits strong predictive capability and aligns well with the data. This relationship is likely due to non-earning individuals, such as children or other dependents, living in the same household as earning individuals.

<p align="center">
<img src="Images/cluster.png" width=700 height=560>
</p>

A cluster analysis was performed using the k-means algorithm to identify groups within the raw data. A scatter plot comparing outreach spending and the proportion of earning individuals segregated outlier data into its own group. I consulted the original dataset and determined that this group represented outreach spending in California. California has spent significantly more on outreach spending than other states. The remaining three cluster groups likely represent the earning, nonearning, and elderly groups.

## Recommendations & Findings
Certain states have consistently high estimated participation rates. The difference between top performing states in 2016 was the presence of policies that grant waivers to allow telephone interviews at initial certification. The presence of this policy became more prevalent at the same time when proportions of earning and non-earning individuals increased.

**Recommendation:** Remove barriers that prevent eligible populations from easily applying and recertifying for SNAP. Individuals should not be penalized because they lack the resources, such as time and transportation, to receive food assistance. Accommodations that consider these limitations for low-income households will encourage participation.

Vermont participation rates were high in 2013, but not in 2011. Policies granting waivers for in-person initial certification interviews were implemented in Vermont for the first time in January 2007, removed in April 2011, and reinstated in September 2012.

**Recommendation:** Policy makers should avoid frequent policy changes because this may be disruptive to eligible populations. Participants could suddenly lose eligibility and it may be difficult for individuals to understand the program's limitations and requirements.

## Next Steps
* Due to time constraints, this analysis focused on states with high estimated participation rates. To provide a more comprehensive understanding of policy influence, extending this analysis to encompass all states could yield additional insights.

* Developing a reliable time series model to forecast the proportions of recipient groups and their recertification periods could promote policies that better accommodate the predominant SNAP recipient groups.

* Augmenting the database with subsequent years' data would enhance the relevance and currency of the insights derived from the analysis.

## Data 
This dashboard uses data from the U.S. Department of Agriculture's (USDA) Economic Research Service (ERS) SNAP Policy Database. This database identifies when certain policies are in effect for each state and the proportions of different SNAP recipient groups. Policy information is obtained from the USDA's Food Nutrition Service (FNS) surveys, policy research organizations, state policy manuals, and news articles. Data collection spans from January 1996 to December 2016 across all 50 states and the District of Columbia. However, some policy details for 2015 and 2016 were unavailable at the time of collection.

The USDA ERS Food Environment Atlas is a collection of data from a variety of sources that identify factors that may influence food choices and diet quality. Percentages of the eligible population participating in SNAP were calculated using estimates of SNAP participants divided by the number of people eligible to participate. Estimates of eligible populations were drawn from the Current Population Survey Annual Social and Economic Supplement and estimates of participants were drawn from SNAP administrative data. A regression model predicted participation rates using data from the American Community Survey, tax returns, population estimates, and administrative records. Different data sources produced different population estimates resulting in some states having predicted rates of 100%, but this should not be interpreted as 100% participation. However, states with significantly high or low estimated rates have consistent estimates.

## Tools & Skills
**Tableau**

**Python Version: 3.11**

Packages: pandas, NumPy, Matplotlib, seaborn, folium, json, sklearn, statsmodels
* Executed data [cleaning](https://github.com/ke177409/SNAP-Policies-and-Participation/blob/main/Scripts/6.1%20Cleaning%2C%20Consistency%20Checks%2C%20%26%20Descriptive%20Analysis.ipynb) and [wrangling](https://github.com/ke177409/SNAP-Policies-and-Participation/blob/main/Scripts/6.2%20Exploring%20Relationships.ipynb) operations prior to analysis.
* Conducted [geospatial analysis](https://github.com/ke177409/SNAP-Policies-and-Participation/blob/main/Scripts/6.3%20Geographic%20Visualization%20Folium.ipynb) using a shapefile to create a choropleth map.
* Performed [regression analysis](https://github.com/ke177409/SNAP-Policies-and-Participation/blob/main/Scripts/6.4%20Supervised%20Machine%20Learning.ipynb) and analyzed model performance statistics.
* Used [elbow technique](https://github.com/ke177409/SNAP-Policies-and-Participation/blob/main/Scripts/6.5%20Unsupervised%20Machine%20Learning.ipynb) to prepare data for cluster analysis using k-means algorithm.
* Tested data for [stationarity](https://github.com/ke177409/SNAP-Policies-and-Participation/blob/main/Scripts/6.6%20Sourcing%20%26%20Analyzing%20Time%20Series%20Data.ipynb) using Dickey-Fuller test and autocorrelation plots.
* Differenced data to ensure stationarity before conducting time-series analysis.

## Data Cleaning & Transformation
Summary of changes and modifications:
* Omitted irrelevant columns "state_pc" and "state_fips".
* Generated dictionaries to assign accurate data types and standardized column names for consistency and clarity.
* Separated year and month values into separate columns for better data organization.
* Checked for mixed data types, missing data, and duplicate entries.
* Defined missing values as time points when policy data was not available at time of data collection.
* Utilized "loc()" function in Python to create categorical columns, such as:
  * "EBT category" to define different percentage levels of benefits allocated through electronic benefit transfers (EBT).
  * "Fingerprint requirement" to identify states with certain fingerprint requirements.

## Purpose & Context
I independently sourced relevant and reliable datasets to educate the general public and policy makers about SNAP. Advanced exploratory analysis techniques were used to gain a deeper understanding of the differences in participation and policies over time. An interactive dashboard was created to easily convey the complexity in the data.

## The Learning Experience
A choropleth map was generated to illustrate the average distribution of reported call centers across the United States. The legend denotes 0 as no call center, 1 as call center present, and 2 as call center situated in specific parts of a state. Unfortunately, the map's effectiveness in this analysis was limited due to the inability to appropriately adjust the color scale.

A time series analysis was conducted to predict the average recertification period for recipient groups, along with the proportions of various recipient groups. Unfortunately, the forecasted trend line did not align well with the actual data. As a result, it was determined that this model might not be suitable or offer valuable insights for this analysis.

## Datasets 
Economic Research Service (ERS), U.S. Department of Agriculture (USDA). SNAP Policy Database, SNAP Policy Data Set. https://www.ers.usda.gov/data-products/snap-policy-data-sets/

Economic Research Service (ERS), U.S. Department of Agriculture (USDA). Food Environment Atlas. https://www.ers.usda.gov/data-products/food-environment-atlas/
