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
- `GradeProgression_LightGBM_model:`: Builds a regression model using LightGBM and hyperparameter optimization using optuna, explains model using SHAP values. 

## Route database analysis





