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
Facebook seems to have the highest engagement rates out of all the platforms.


**2.** Found how many posts had an engagement rate greater than 0.75 and had a positive sentiment label.
```{r}
highPositive <- filter(socialMedia,
       sentiment_label == "Positive" &
         engagement_rate >= 0.75)
```
```{r}
nrow(highPositive)
```
There are 244 posts that meet both of those filters.


**3.** Found the emotion type with the lowest engagement rate.
```{r}
emotionEngagement <- group_by(socialMedia, emotion_type)
summarise(emotionEngagement,
          avgEngagement = mean(engagement_rate, na.rm = TRUE) * 100) %>%
  arrange(avgEngagement)
```

### Statistical Analysis

**Descriptive Statistics**

Several descriptive statistics were calculated to better understand the engagement patterns within the dataset.
  - The mean engagement rate was about **27%** across all social media posts.
  - The median shows that the middle number of likes received across all social media posts in the dataset is **2,496**.
  - The minimum likes count was **0** and maximum was **5,000**. This shows a large range between post performances.

**Hypothesis Testing**

A two-sample t-test was done to determine if positive sentiment posts receive higher engagement rates compared to negative sentiment posts.

**Hypotheses**
  - Null Hypothesis (H0): There is no difference in engagement rates between positive and negative posts.
  - Alternative Hypothesis (H1): There is a difference in engagement rates between positive and negative posts.

**t-Test**
```{r}
t.test(engagement_rate ~ sentiment_label,
       data = sentimentTest)
```

**Results**
With the p-value being greater than 0.05, we fail to reject the null hypothesis. There is an insignificant amount of evidence to show that engagement rates differ between positive and negative posts.

### Data Visualizations
