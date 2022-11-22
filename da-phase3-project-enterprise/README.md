# Phase 3 Project

## Project Overview

For this project, you will use data cleaning and inferential statistics to produce a report about the provided dataset.

### The Data

This project uses health data from the [CDC Behavioral Risk Factor Surveillance System (BRFSS)](https://www.cdc.gov/brfss/data_documentation/index.htm). Specifically this subset of the data represents survey responses from the 2020-2021 survey in the state of New York. Each record represents a survey response.

![tissues and tea mug](https://raw.githubusercontent.com/learn-co-curriculum/da-phase3-project-enterprise/main/sick_day.jpg)

Photo by <a href="https://unsplash.com/@kellysikkema?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Kelly Sikkema</a> on <a href="/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

The main variable of interest in this dataset is `PHYSHLTH`. This column represents the answer to this question:

> Now thinking about your physical health, which includes physical illness and injury, for how many days during the past 30 days was your physical health not good?

The complete codebook (data dictionary) from the CDC is available [here](https://www.cdc.gov/brfss/annual_data/2020/pdf/codebook20_llcp-v2-508.pdf).

### Requirements

#### 1. Prepare Data for Statistical Analysis

At minimum, perform data cleaning for the `PHYSHLTH` and `RENTHOM1` columns.

Given that the question in the `PHYSHLTH` column is asking about "how many days during the past 30 days", you might assume that the values in this column will all be numbers between 0 and 30.

However, this is not the case. If you plot a histogram of values you'll see that many values are higher than 30. In fact, the mean is around 67!

The reason for this is that **the survey was designed to use certain numbers as "codes" rather than actual values**.

The codebook gives us this information:

```
| Value  | Value Label          |
| ------ | -------------------- |
| 1 - 30 | Number of days       |
| 88     | None                 |
| 77     | Don't know/Not sure  |
| 99     | Refused              |
| BLANK  | Not asked or Missing |
```

Therefore you should prepare the data in `PHYSHLTH` by:

* Converting all instances of `88` to `0`
* Dropping all records where `PHYSHLTH` is `77`, `99`, or blank (NaN)

We are also interested in demographic features, such as the `RENTHOM1` question:

> Do you own or rent your home?

Once again, this is represented somewhat confusingly in the data. The codebook tells us this:

```
| Value | Value Label          |
| ----- | -------------------- |
| 1     | Own                  |
| 2     | Rent                 |
| 3     | Other arrangement    |
| 7     | Don't know/Not Sure  |
| 9     | Refused              |
| BLANK | Not asked or Missing |
```

Prepare the data by dropping records with values of `RENTHOM1` other than 1 or 2.

#### 2. Calculate Confidence Interval for `PHYSHLTH` Mean

How many days of poor physical health did New Yorkers typically have in 2020-2021? To answer this question, calculate the mean of `PHYSHLTH`.

This survey contains over 10,000 responses, but there were more than 20 million people living in New York State in 2020 according to the US Census. So instead of simply reporting the mean, calculate and report a 95% confidence interval around the mean.

Your notebook should include **both the numeric result and a written interpretation**.

#### 3. Describe Difference in `PHYSHLTH` Based on `RENTHOM1`

Separate the records based on the value of `RENTHOM1` (i.e. whether the person owns or rents their home).

Then produce one or more plots that demonstrate the value of `PHYSHLTH` within each subset. The exact type of plot is up to you. Some examples to consider include histograms showing the distribution of `PHYSHLTH` for each subset, or a bar graph that shows the mean of each subset (with or without confidence intervals).

In addition to your plot, include a written interpretation of what you see.

#### 4. Perform t-Test on `PHYSHLTH` Based on `RENTHOM1`

Is the difference in `PHYSHLTH` based on whether someone rents or owns their home statistically significant? Perform a t-test to answer this question. Use the typical alpha value of 0.05.

Make sure you include all of the relevant elements of a t-test:

* **Describe null and alternative hypotheses**
  * It is up to you whether you want to define this as two-tailed (the means are different) or one-tailed (one particular mean is greater than the other)
* **Calculate the test statistic and p-value**
  * Remember that you can use `scipy.stats` for this
* **Interpret the result**
  * Can we reject the null hypothesis at an alpha of 0.05?

#### 5. Describe Next Steps

Given the above information, what feature of the dataset would you propose investigating next?

**You do not need to investigate another feature, just describe your plan.**

Use the [CDC codebook](https://www.cdc.gov/brfss/annual_data/2020/pdf/codebook20_llcp-v2-508.pdf) to select a variable and explain how you would use it to investigate further.

## Deliverables

Your deliverable for this project is a **Jupyter Notebook** (`.ipynb` file). Click on the button to open the starter notebook in IllumiDesk, then edit the code and Markdown cells to complete the project requirements.

Make sure you save your work regularly!

When you are ready to submit the project for grading, download the notebook and submit it using this Canvas assignment.

## Grading

The below rubric will be used for grading. There are 10 total points for this project.

To summarize, you get:

* 1 point for **data cleaning on `PHYSHLTH`**
  * This means that there are no missing values in `PHYSHLTH` and no values less than 0 or greater than 30
* 1 point for **data cleaning on `RENTHOM1`**
  * This means that there are only two values in `RENTHOM1`, representing whether the respondent said they owned or rented their home
* 2 points for a **confidence interval about the mean of `PHYSHLTH`**
  * 1 point for calculating the confidence interval
  * 1 point for interpreting the confidence interval
* 2 points for a **description of the differences in `PHYSHLTH` based on `RENTHOM1`**
  * 1 point for creating a plot
  * 1 point for interpreting the plot
* 3 points for **setting up, executing, and interpreting a t-test**
  * 1 point for describing null and alternative hypotheses
  * 1 point for calculating the test statistic and p-value
  * 1 point for interpreting the result
* 1 point for **describing next steps**
  * Specifically you need to refer to the [CDC codebook](https://www.cdc.gov/brfss/annual_data/2020/pdf/codebook20_llcp-v2-508.pdf) and pick another column that you would investigate next
