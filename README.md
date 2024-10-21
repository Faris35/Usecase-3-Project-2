# Usecase-3-Project-2

## Project Overview
This project aims to analyze world university rankings using the dataset from Kaggle. We will address key problem statements related to global and national university rankings and their factors.

### Problem Statements
In this project, we will explore the following questions:

1. **Top 10 Global Universities**: Which universities are ranked in the top 10 globally?
2. **Top 10 Employment Outcomes**: Which universities are ranked in the top 10 for employment outcomes?
3. **Saudi Arabian Universities**: What positions do universities in Saudi Arabia hold within the global rankings?
4. **Impact of Various Factors**: Considering various factors such as employment rankings, research rankings, and others, which has the most significant impact on a university's overall ranking?
5. **Correlation Between Rankings**: Is there a correlation between national and global university rankings? Based on this information, can you recommend a country that has a high concentration of top-ranked universities?

### Steps to Complete the Project
#### Step 1: Defining the Problem Statement

We have outlined specific questions that will guide our analysis and research throughout the project.


#### Step 2: Collecting Data

This is the most important step because you can't complete your work without data. The project uses specific datasets collected from the [Kaggle website](https://www.kaggle.com/datasets/ourfuture/world-university-rankings).

*About Dataset*: The dataset contains universities' world and national rankings and also employability and education rankings and other features we will recognize later.


#### Step 3: Exploratory Data Analysis
In this step, we will conduct an exploratory analysis to uncover patterns, trends, and insights.

**Import libraries**
Import all relevant libraries before starting **EDA**.
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import zscore
import regex as re
 
## This statement allows the visuals to render within your Jupyter Notebook.
%matplotlib inline
```
#### Key Aspects of EDA:
**Data Profiling:**
- Descriptive Analysis

**Loading the data**

```python
shanghai_rank = pd.read_excel('shanghai Ranking.xlsx') #ARWU
times_h = pd.read_excel('Times Higher Education.xlsx') #THE
word_rank = pd.read_excel('Word Rank University.xlsx') #CWUR
```

**Viewing the dataframe**
```python
print(f"Shanghai Ranking DataFrame shape: {shanghai_rank.shape}")
print(f"Times Higher Education DataFrame shape: {times_h.shape}")
print(f"World Rank University DataFrame shape: {word_rank.shape}")
```
```markdown
Shanghai Ranking DataFrame shape: (1000, 6)
Times Higher Education DataFrame shape: (1591, 20)
World Rank University DataFrame shape: (2000, 9)
```
As we see the highest number of rows exists in *World Rank University* dataset and that describes this dataset as more than comprehensive the other datasets.

**Displaying the columns for each DataFrame**
```python
# We will see columns in each dataframe
print(f"Shanghai Ranking DataFrame columns: {' - '.join([col for col in shanghai_rank.columns])}")
print()
print(f"Times Higher Education DataFrame columns: {' - '.join([col for col in times_h.columns])}")
print()
print(f"World Rank University DataFrame columns: {' - '.join([col for col in word_rank.columns])}")
```
```markdown
Shanghai Ranking DataFrame columns: Ranking - University Name - National/Regional Rank - Total Score - LOGO - University Detail 

Times Higher Education DataFrame columns: Rank - University Name  - ranking-institution-title href - Location - sdg-score-multi__number - sdg-score-multi__value - sdg-score-multi__number 2 - sdg-score-multi__value 2 - sdg-score-multi__number 3 - sdg-score-multi__value 3 - sdg-score-multi__value 4 - scores - sdg-score-multi__number 5 - sdg-score-multi__value 5 - sdg-score-multi__number 6 - sdg-score-multi__value 6 - sdg-score-multi__number 7 - sdg-score-multi__value 7 - sdg-score-multi__number 8 - sdg-score-multi__value 8

World Rank University DataFrame columns: World Rank - University Names - Location  - National Rank - Educational Rank - Employability Rank - Faculty Rank - Research Rank - Score
```
**Note!**: The following EDA steps will be applied mostly in the World Rank University dataset.

```python
print("World Rank University information:-\n")
word_rank.info() # Information about the dataframe
word_rank.describe(include=['object']) # Object columns description
```

```markdown
World Rank University information:-

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2000 entries, 0 to 1999
Data columns (total 9 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   World Rank          2000 non-null   object 
 1   University Names    2000 non-null   object 
 2   Location            2000 non-null   object 
 3   National Rank       2000 non-null   int64  
 4   Educational Rank    2000 non-null   object 
 5   Employability Rank  2000 non-null   object 
 6   Faculty Rank        2000 non-null   object 
 7   Research Rank       2000 non-null   object 
 8   Score               2000 non-null   float64

dtypes: float64(1), int64(1), object(7)
memory usage: 140.8+ KB
```

|           | World Rank      | University Names                               | Location | Educational Rank | Employability Rank | Faculty Rank | Research Rank |
|-----------|-----------------|------------------------------------------------|----------|------------------|-------------------|--------------|----------------|
| count     | 2000            | 2000                                           | 2000     | 2000             | 2000              | 2000         | 2000           |
| unique    | 2000            | 2000                                           | 95       | 439              | 1030              | 262          | 1935           |
| top       | 1Top 0.1%      | Harvard University\nCWUR Rating System: Ed... | USA      | -                | -                 | -            | -              |
| freq      | 1               | 1                                             | 332      | 1562             | 967               | 1727         | 66             |

From this table, we can figure out many things: 
1. World Rank contains a string so we need to deal with it and convert it to int
2. The USA is the most the country appearance in the World Rank
3. There is no duplication in University Names column so that is good
4. Educational Rank - Research Rank the most duplication is a dash "-", so that indicates columns contain null values


                               
**Step 4: Communicating Results**


