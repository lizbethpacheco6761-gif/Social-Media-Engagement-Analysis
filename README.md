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


**Linear Regression**

A linear regression model was created to determine whether sentiment score could predict engagement rate on social media posts.

**Model**
```{r}
engagement_lm <- lm(engagement_rate ~ sentiment_score,
                    data = socialMedia)

summary(engagement_lm)
```


**Results**

The model shows that the sentiment score cannot predict engagement rate. The p-value also shows a weak connection, sentiment scores does not affect engagement rate.


### Data Visualizations

*Average Engagement by Platform*

This bar chart compares the average engagement rate across different social media platforms.

<img width="823" height="450" alt="image" src="https://github.com/user-attachments/assets/cd145daf-d23e-4d3e-8727-b84413af7964" />


*Sentiment Score vs Engagement Rate*

This scatter plot visualizes the relationship between sentiment score and engagement rate.

<img width="823" height="450" alt="image" src="https://github.com/user-attachments/assets/ffa12ab5-67f4-48bf-8a7a-8a621ba24ebb" />

*Average Engagement Rate by Emotion Type*

This bar chart compares the average engagement rate across different emotion types within the dataset.

<img width="823" height="450" alt="image" src="https://github.com/user-attachments/assets/57c4a0a6-2cf7-4763-be81-8baa0a6c736d" />


### Conclusion
This project helped me explore how platform type, emotion type, and sentiment score relate to social media engagement rates. After cleaning and analyzing the data in R, I found that engagement levels varied across posts, but sentiment score was not a strong predictor of engagement.
