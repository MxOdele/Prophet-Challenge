# Prophet-Challenge

<div align='center'>
    <img src='https://download.logo.wine/logo/MercadoLibre/MercadoLibre-Logo.wine.png' height='300' title='The Mercado Libre logo (image courtesy of Logo Wine)' alt='An image of the Mercado Libre logo, two hands shaking over a yellow background with blue trim and the company name written below' />

*Prophet Challenge*[^1]

## Read Me

# README Still In Progress Of Being Written
</div>

## Table of Contents

* [Overview](#Overview)
* [Execution](#Execution)

---

## Overview

### *The Assignment*

For our Week 8 Challenge we were tasked with completing the provided Jupyter Notebook `forecasting_net_prophet.ipynb` to 

1. Step
    * Substep

### *Written in*

Jupyter Notebook using Python v3.10.13, Pandas, Prophet, and Google Colaboratory

### *Accessing the notebook*

To access the {NOTEBOOK} notebook, simply download the `.ipynb` file `forecasting_net_prophet.ipynb` and {ANYTHING ELSE?} in this repository into one directory, then upload the `forecasting_net_prophet.ipynb` file to your Google Drive, open with Google Colab.

---

## Execution

### *How to use*

Simply execute `Run All` from the `Runtime` menu to execute the code in every cell of the notebook in sequence. Alternatively, each cell may be `Run` on its own, though it is still recommended to run them in order.

### *Breaking down the cells*

Below is a more in-depth explanation of the various cells coded within the `forecasting_net_prophet.ipynb` notbook.

| Cell (in order from top to bottom) | Notes[^2] (on the contained code) |
| ---: | :--- |
| 1[^3] | Installing required libraries |
| 2[^3] | Importing required libraries and dependencies |
| 3[^3] | Reading in data for `df_mercado_trends` DF <br> *`Date` used as index with Datetime values* <br> *Empty rows dropping during read in* <br> Reviewing first and last five (5) rows |
| 4[^3] | Reviewing data types for `df_mercado_trends` |
| 5 | Declaring `df_may_2020` as a slice of `df_mercado_trends` with only rows from May of 2020 <br> Plotting the sliced data |
| 6 | Declaring `traffic_may_2020` as the `.sum()` of `df_may_2020` <br> Viewing the value for `traffic_may_2020` |
| 7 | Declaring `median_monthly_traffic` as the `.median()` of the month by year from `df_mercado_trends` <br> *Values for `.median()` based on `.sum()` of same data* <br> Viewing the value for `median_monthly_trffic` |
| 8[^3] | Comparing the value of `traffic_may_2020` to the value of `median_monthly_trffic` |
| Q1 | **Question:** <br> Did the Google search traffic increase during the month that MercadoLibre released its financial results? <br> **Answer:** <br> Yes, by a value of over 3,000 as compared to the median value for all months |
| 9[^4] | Grouping and plotting the hourly data from `df_mercado_trends` |
| 10[^4] | Grouping and plotting the daily data from `df_mercado_trends` |
| 11[^4] | Grouping and plotting the weekly data from `df_mercado_trends` |
| Q2 | **Question:** <br> Are there any time based trends that you can see in the data? <br> **Answer:** <br> Yes. <br> In terms of hours, traffic tends to peak around midnight. <br> In terms of days, traffic tends to peak on Tuesdays. <br> In terms of weeks, mid-late January through most of February (roughly the second (2nd) through eighth (8th) weeks) tend to see the most traffic. <br> Ultimately, this would imply that around midnight on Tuesdays in the early year will see the most traffic. |
| 12[^3] | Reading in data for `df_mercado_stock` DF <br> *`Date` used as index with Datetime values* <br> *Empty rows dropping during read in* <br> Reviewing first and last five (5) rows |
| 13 | Visualizing the data for `df_mercado_stock` |
| 14 | Declaring `mercado_stock_trends_df` as the concatenation of `df_mercado_stock` and `df_mercado_trends` <br> *Empty rows dropping during joining* <br> Reviewing first and last five (5) rows |
| 15 | Declaring `first_half_2020` as a slice of `mercado_stock_trends_df` for 2020-01 through 2020-06 <br> Reviewing first and last five (5) rows |
| 16[^4] | Visualizing the data for `first_half_2020` with each column on its own subplot |
| Q3 | **Question:** <br> Do both time series indicate a common trend that’s consistent with this narrative? <br> **Answer:** <br> Yes and no. Both datasets indicate a drop from late February through March. While the `Close` remained low through April, however, `Search Trends` had a spike in late March to early April. That said, a surge in `Search Trends` in May (as discussed in Step 1) corresponds with a jump in `Close` to previous highs. That said, while `Close` continued to rise through June, `Search Trends` experiences a relatively minor lull followed by a much smaller peak. <br> As such, it is fair to say that there are trends that are consistent with the narrative outlined above in Step 2. |
| 17 | Adding column `Lagged Search Trends` to `mercado_stock_trends_df` as a `.shift()` of `Search Trends` column <br> Reviewing the first three (3) rows to confirm `.shift()` applied correctly |
| 18 | Adding column `Stock Volatility` to `mercado_stock_trends_df` as a `.std()` of `close` column <br> Reviewing the first five (5) rows to confirm `.std()` applied correctly |
| 19 | Visualizing the data for the `Stock Volatility` column of `mercado_stock_trends_df` |
| 20 | Adding column `Hourly Stock Return` to `mercado_stock_trends_df` as a `.pct_change()` of `close` column <br> Reviewing the first three (3) rows to confirm `.pct_change()` applied correctly |
| 21 | Reviewing first and last five (5) rows of `mercado_stock_trends_df` |
| 22[^3] | Correlating the values of the `Stock Volatility`, `Lagged Search Trends`, and `Hourly Stock Return` columns of `mercado_stock_trends_df` |
| Q4 | **Question:** <br> Does a predictable relationship exist between the lagged search traffic and the stock volatility or between the lagged search traffic and the stock price returns? <br> **Answer:** <br> `Lagged Search Trends` seems to have a weak negative correlation with `Stock Volatility`, and an exceptionally weak negative correction with `Hourly Stock Return`. While `Stock Volatility` might decrease slightly as `Lagged Search Trends` increases, there is nothing to suggest a concrete and reliable relationship between the two values. Even less so for `Lagged Search Trends` and `Hourly Stock Return`. <br> So no, no predictable relationship exists between `Lagged Search Trends` and `Stock Volatility` or `Hourly Stock Return`. |
| 23 | Declaring `mercado_prophet_df` as `df_mercado_trends` with a reset index <br> Renaming the columns of `mercado_prophet_df` to `ds` and `y` in preparation of Prophet <br> Reviewing first and last five (5) rows |
| 24 | Declaring `m` as `Prophet()` |
| 25 | Fitting `mercado_prophet_df` to Prophet |
| 26 | Declaring `future_mercado_trends` to predict out approximately eighty (80) days <br> Reviewing last five (5) rows |
| 27 | Declaring `forecast_mercado_trends` as a prediction from `future_mercado_trends` <br> Reviewing last five (5) rows |
| 28 | Plotting the predictions from `forecast_mercado_trends` using `m.plot()` |
| Q5 | **Question:** <br> How's the near-term forecast for the popularity of MercadoLibre? <br> **Answer:** <br> I looks like there is to be a moderate decline in MercadoLibre's popularity coming into October. After hitting a low point, the popularity should begin to increase back towards previous levels. |
| 29 | Setting the index of `forecast_mercado_trends` to `ds` column <br> Reviewing last five (5) rows for the `yhat`, `yhat_lower`, and `yhat_upper` columns |
| 30 | Plotting the the rows for the last two-thousand (2,000) hours of the `yhat`, `yhat_lower`, and `yhat_upper` columns of `forecast_mercado_trends` |
| 31 | Resetting the index for `forecast_mercado_trends` <br> Plotting the components of `forecast_mercado_trends` with `m.plot_components()` |
| Q6 | **Question:** <br> What time of day exhibits the greatest popularity? <br> **Answer:** <br> Around midnight |
| Q7 | **Question:** <br> Which day of week gets the most search traffic? <br> **Answer:** <br> Tuesdays |
| Q8 | **Question:** <br> What's the lowest point for search traffic in the calendar year? <br> **Answer:** <br> Sometime in early- to mid-October |

[^1]: Image courtesy of <a href='https://www.logo.wine/logo/MercadoLibre' title='Link to Logo Wine listing for image'>Logo Wine</a>

[^2]: Markdown cells with questions and answers are annotated, however, Markdown cells for instructions ***NOT*** annotated

[^3]: Executable code provided in starter file, not written by student

[^4]: Comments in cell contained portion of code in starter file as prompt for student, executable code written by student