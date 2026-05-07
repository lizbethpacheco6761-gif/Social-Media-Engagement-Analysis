# Social-Media-Engagement-Analysis

### Data
The dataset worked on was the *Social Media Engagement Dataset* from Kaggle.
https://www.kaggle.com/datasets/subashmaster0411/social-media-engagement-dataset


### Project Overview
As an avid scroller, I wanted to find a dataset related to social media.  
In this project, many factors were taken into consideration to see the affects on engagement rates on different platforms.  In the project, the data was cleaned, manipulated, analyzed, and visualized to see trends within the dataset.  Statistical analysis and linear regression were also used to better understand the relationship between the sentiment score and engagement rate.

### Importing Data
The dataset was imported into R using the **read_excel()** from the tidyverse package. 
After looking over the data, three main focuses were determined.
  - Which social media platform had the highest engagement rate?
  - Does a higher sentiment score lead to a higher engagement rate?
  - Which emotion type sees the lowest engagement?

### Data Cleaning
Prior to the analysis beginning, the dataset was checked for missing and duplicated values. All but one variable saw 0 missing values. *Mentions* has 3,941 missing values, but since it won't affect the analysis, there will be no change. There was 0 duplicates in the data.

### Data Manipulation
Data was manipulated using dplyr functions.
**1.** Found the average engagement rate by platform
```{r}
platformEngagement <- group_by(socialMedia, platform)
summarise(platformEngagement,
          avgEngagement = mean(engagement_rate, na.rm = TRUE) * 100)
```
### Statistical Analysis

### Data Visualizations
