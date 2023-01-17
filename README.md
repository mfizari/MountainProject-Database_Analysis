# MountainProject-Database-Analysis

This repository contains data scraped from Mountainproject.com and code used for analytics and model building. <br/>
The repository contains 2 directories:<br/>

#### Data <br/>
Contains raw and processed route data and user data produced by the code in the `MountainProject-Scraper` repository. There are 3 files: <br/>
- `routedata.jl`: Information on each route page, produced by the scraper. <br/>
- `userdata_filter.json`: User tick data for the subset of users with more than 100 ticks. This is produced by the notebook `Preprocess_FilterUsers` given the 
entire (~1.8 GB) `userdata.jl` file produced by the scraper. <br/>
- `userdata_formatted.json`: Features and target variable for tick progression regression model, produced by the notebook `Preprocess_UserProgression` <br/>

#### Notebooks <br/>
Contains Jupyter notebooks for analysis and model building and a directory for figures. The notebooks are as follows: <br/>
- `RouteStatistics`: Summary of various statistics for the route database from `routedata.jl`. <br/>
- `Preprocess_FilterUsers`: Filters large `userdata.jl` file by tick number and outputs new file as above. <br/>
- `Preprocess_UserProgression`: Reduces user data into a set of summary statistics for each user's tick log (progression correlation, fraction of each style climbed, demographic information, etc) and outputs new file as above. <br/>
- `GradeProgression_LightGBM_model`: Builds a regression model using LightGBM and hyperparameter optimization using optuna, explains model using SHAP values. 


## Progression modeling: What you should do in order to get better at climbing
The results of the regression model for consistency of progression (found in `GradeProgression_LightGBM_model`) can help us inform users on ways they might be able to improve their progression. Our suggestions should be guided by the importance of each feature and it's directionality on the output. First, we'll use SHAP values to visualize the strength and directionality of each feature's influence on our model output:

![alt text](https://github.com/mfizari/MountainProject-Database_Analysis/blob/main/Notebooks/Figures/beeswarm.png)

We see that indicators of a climber's tendency to push themselves (redpointing, falling, bouldering) increase the strength of progression. Additionally, features relating to climber's volume of climbing (FractionDaysClimbing, NumberTicks) increase progression, but AccountAge does not, confirming the old adage - "it's not the years, it's the mileage". The relative importance of the different types of features are shown below:

![alt text](https://github.com/mfizari/MountainProject-Database_Analysis/blob/main/Notebooks/Figures/importance.png)

Lastly, the SHAP dependence plots indicate that many of the relationships are nonlinear, which affects the suggestions we make for improvement. For example, the output dependence on type features and style features:


![alt text](https://github.com/mfizari/MountainProject-Database_Analysis/blob/main/Notebooks/Figures/Style_SHAP.svg)


## Route database analysis
There are a lot of analytics that can be done on route and user data scraped from MountainProject. One thing I was interested in investigating was how the relative prevelance of different types of routes in the US has changed with time. I looked at the data and found that bouldering has been becoming increasingly popular over the last decade (with a large surge during the first year of COVID), and now the majority of routes on MountainProject are boulders. The data is visualized in a static Tableau dashboard: 

![alt text](https://github.com/mfizari/MountainProject-Database_Analysis/blob/main/Notebooks/Figures/GrowthOfBouldering.png)



