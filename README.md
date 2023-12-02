# SNAP Policies and Participation: Project Overview
Analyzed data from the Supplemental Nutrition and Assistance Program (SNAP) Policy Database to detect changes in state policies and participation rates over time. Insights include changes within SNAP recipient groups, relationships between different groups of SNAP recipients, relationships between different policies, and identification of policies that might influence participation rates. Python was used to clean data, perorm exploratory analysis, and create data visualizations to detect relationships between different variables. Tableau was used to create a comprehensize dashboard and additional visualizations that provide more detail.

## Tools & Skills
Python Version: 3.11
Tableau

Packages: pandas, NumPy, Matplotlib, seaborn, folium, json, sklearn, pylab, statsmodels
* Executed data wrangling and merging operations.
* Conduct geospatial analysis using a shapefile to create a choropleth map.
* Perform linear regression analysis and analyze model performance statistics.
* Use elbow technique to prepare data for cluster analysis using k-means algorithm.
* Test for stationarity in data using Dickey-Fuller test and autocorrelation plots.
* Perform differencing to stationaritze data prior to time-series analysis.

## Purpose & Context
I independently sourced relevant and reliable data to educate the general public and policy makers about SNAP. Advanced exploratory analysis techniques were used to gain a deeper understanding of the differences in participation and policies over time. An interactive dashboard was created to easily convey the complexity in the data.

## Data Cleaning & Transformation
Following a comprehensive descriptive analysis of the data, I identified several areas where data cleaning and transformation were necessary. Here's a summary of the changes and modifications that were made:

* Columns "state_pc" and "state_fips" were dropped due to irrelevant data.
* Dictionaries were created to assign appropriate data types.
* Column names were systematically renamed to enhance clarity and ensure consistency.
* Separated year and month values into separate columns.
* A thorough check for mixed data types, missing data, and duplicate entries was conducted.
* Missing values in data set represent time points when policy data was not available at time of data collection.
* The "loc()" function in Python was used to create categorical columns such as:
  * "EBT category" to define when states issued different percentage levels of benefits using electronic benefit transfers.
  * "Fingerprint requirement" to flag which states had certain fingerprint requirements.

## Visualizations
The correlation heatmap was created in Python using the seaborn heatmap to identify relationships within the data and understand how certain variables influence each other. Five policies had significant correlations with each other. 

Broad-based categorical eligiblity (BBCE) allows states to increase income and asset eligibility limits for low-income households. BBCE had a moderate positive correlation (0.59) with policies that do not limit the number of household vehicles when measuring assets. 

Policies that do not limit the number of household vehicles and offered the simplified reporting option had a slightly stronger correlation (0.61). Simplified reporting reduces the requirements for reporting changes in household circumstances. 

Policies that allow telephone interviews (instead of face-to-face interviews) at initial certification had a moderate positive correlation with policies that allow households to apply for SNAP online (0.59). 

<p align="center">
<img src="CORRHEATMAP" width=370 height=330>
</p>

A positive linear relationship was detected between earning and nonearning individuals with 7 to 12 month recertification periods (0.89). I hypothesized that as earning proportions increase, nonearning proportions will also increase. A linear regression analysis was performed to assess how the proportions of earning individuals influences the proportions of nonearning individuals. The mean squared error for the training set was 0.0339 and the R2 score was 0.7973. This model is a good fit for the data and validated my hypothesis. This relationship is likely due to nonearning individuals, such as children or other dependents, live within the same household as earning individuals. 

<p align="center">
<img src="REGRESSION" width=370 height=330>
</p>

The EBT categorical plot was created to plot the different dollar percentages issued using EBT. I found that beginning in most of 2004 and onward, at least 80% of SNAP benefits were accounted by EBT in all states. 
<p align="center">
<img src="EBTCATPLOT" width=370 height=330>
</p>

The fingerprint categorical plot was created to show which states reported certain fingerprint requirements. States could report "not required", "required in parts of state", or "required". Arizona, California, Massachusetts, New York, and Texas have reported fingerprint requirements for SNAP applicants.
<p align="center">
<img src="FINGERPRINT" width=370 height=330>
</p>

A cluster analysis was performed using the k-means algorithm in an attempt to identify other groups not detected in the raw data. A scatter plot comparing outreach spending and the proportion of earning individuals showed some outlier data that was assigned its own group. I determined that this group represented outreach spending for the state of California. This was confirmed against the raw data, which showed that California has spent significantly more on outreach spending than other states. I also determined that the other three cluster groups most likely represent the earning, nonearning, and elderly groups.

<p align="center">
<img src="CLUSTER" width=370 height=330>
</p>

## Recommendations & Findings
Based on the insights derived from the analysis, several recommendations can be made:

* Some states have consistently high estimated participation rates. The difference between the top performing states in 2016 was the presence of policies that grant waivers to allow telephone interviews at initial certification. The presence of this policy became more prevalent at the same time when there was a large increase in proportions of earning and nonearning individuals. Remove barriers that prevent eligible populations from easily applying and recertifying for SNAP. Individuals should not be penalized because they lack the resources, such as time and transportation, to receive food assistance. Accomodations that consider these limitations for low-income households will encourage participation.

* Vermont participation rates were high in 2013, but not in 2011. Policies granting waivers for in-person initial certification interviews was implemented in Vermont for the first time in January 2007, removed in April 2011, and reinstated in September 2012. Policy makers should avoid repeated changes in policies because this may be disruptive to eligible populations. Participants could lose their eligibility and it may be difficult for individuals to understand the program's limitations and requirements.

## The Learning Experience
A choropleth map was created to show where call centers are reported on average throughout the United States. The use of this map was not useful for this analysis. The color scale does not accurately reflect the binary data that it's meant to represent (0 = no call center, 1 = call center, 2 = call center in parts of the state).

A time series analysis was performed to attempt to forecast the average number of months recipient groups will need to recertify. This was also performed on the proportions of different groups. However, the forecasted line did not fit the actual data, so I decided that this model may not be a good fit or provide any valuable information to this analysis.

## Datasets 
Economic Research Service (ERS), U.S. Department of Agriculture (USDA). SNAP Policy Database, SNAP Policy Data Set. https://www.ers.usda.gov/data-products/snap-policy-data-sets/

Economic Research Service (ERS), U.S. Department of Agriculture (USDA). Food Environment Atlas. https://www.ers.usda.gov/data-products/food-environment-atlas/
