# Risk-Return Analysis Application
## Introduction
This application is used to determine (4) different investment funds with the most potential. The investment funds that are being analyzed are Soros Fund Management, Paulson & Co. Inc., Tiger Global Management and Berkshire Hathaway Inc along with analysis of the S&P 500 index. This application will use several key-risk management metrics such as daily percent change, standard deviation, Sharpe ratio and Beta.

---

## Technologies

The following technology/software was used for this application:


-Python 3.7.11 (Programming language)

    Imported Python Libraries/Packages:
    
    -Path from pathlib
    
    -csv
    
    -Pandas as pd
    
    -import numpy as np
    
    -import seaborn as sns
    
    -%matplotlib inline
    
-JupyterLab

-Git version 2.34.11.windows.1

-Windows 10 Operating System

---

## Installation Guide

To install this application on your machine, download (or clone using http link) all files contained in this repository davidlp94/04_Risk_Return_Analysis.

Next, open GitBash (terminal for MacOS), change your directory to the 04_Risk_Return_Analysis, open JupyterLab in a dev environment and open/run the risk_return_analysis.ipynb file.

---

## Usage

This Risk_Return_Analysis application contains the following files/directories:
```
.ipynb_checkpoints/ - This directory contains checkpoint/auto-save files.
Reources/ - This directory contains a .csv file with historical data on the (4) investment funds as well as S&P 500.
risk_return_analysis.ipynb - This file contains the main source code for this application and can be ran in JupyterLab.
README.md - A README file that contains an overview of this application.
license.txt
```

---

## Main Source Code

This application has 5 parts:
```
Part 1 - Analyzing the Performance
Part 2 - Analyzing the Volatility
Part 3 - Analyzing the Risk
Part 4 - Analyzing the Risk-Return Profile
Part 5 - Diversifying the Portfolio
```
Before we get into the main application, our very first step is to import the .csv file, combine into one dataframe and calculate the daily_pct_change and drop any NaN values.
```
whale_funds_sp500_df = pd.read_csv(
    Path('Resources/whale_navs.csv'),
    index_col='date',
    infer_datetime_format=True,
    parse_dates=True
)
whale_funds_sp500_df.head()

daily_returns = whale_funds_sp500_df.pct_change().dropna()
```
---
### Part 1 - Analyzing the Performance

Using the Pandas .plot() and .cumprod() function, we can generate and analyze the data in a line plot.
```
daily_returns.plot(figsize=(25, 25), title='Whale Funds vs. S&P500', ylabel='pct_change')
cumulative_returns = (1 + daily_returns).cumprod()
cumulative_returns.plot(figsize=(15, 7), title='Cumulative Returns of Whale Funds vs. SP500', xlabel='Date', ylabel='Cumulative Return')
```
The following plots are generated:
![image](https://user-images.githubusercontent.com/96163075/151414698-bdd94861-3f78-4f17-8fe7-1fe194d33669.png)
![image](https://user-images.githubusercontent.com/96163075/151414772-5902dcbe-d8e9-4d40-8abd-80696e897bc2.png)

Based on the above Cumulative Return plot, none of the portfolios outperform the S&P 500 index. Berkshire Hathaway had roughly a 23.6% cumulative return from NAV but is much less than the S&P500 71.8% cumulative return from NAV.

---

### Part 2 - Analyzing the Volatility

Using the Pandas .plot() function with a parameter of kind="box", we can generate a box plot to visualize the volatility of the daily percent change. Additionally, we can use the .drop() function to remove the S&P 500 data and just visualize the (4) investment funds we are analyzing.
```
daily_returns.plot(kind='box', figsize=(15, 7), title='Daily Return of Whale Funds', xlabel='Asset', ylabel='Daily Return Percentage')

whale_funds_df = whale_funds_sp500_df.drop(columns=['S&P 500'])
daily_return_whale_funds = whale_funds_df.pct_change().dropna()
daily_return_whale_funds.plot(kind='box', figsize=(15, 7), title='Daily Return of Whale Funds', xlabel='Asset', ylabel='Daily Return Percentage')
```
![image](https://user-images.githubusercontent.com/96163075/151416005-f6bd1419-4c93-43f5-9cd1-ee4ce3ad64a2.png)
![image](https://user-images.githubusercontent.com/96163075/151416045-f4f25a34-e6f2-4569-a04f-84fb7db34785.png)

Based on the box plot above, the most volatile fund was Berkshire Hathwaway Inc and the least volatile fund was Tiger Global Management LLC.

---

### Part 3 - Analyzing the Risk

In this section, we will evaluate the risk of each investment fund using the Pandas by calulating the standard deviation using the .std() function as well as calculating the annualized standardized deviation using the np.sqrt() function. Finally, using the .rolling() function, we can plot the rolling standard deviation using a 21-day rolling window.

```
standard_deviation = daily_returns.std().sort_values()
standard_deviation

trading_days = 252
annual_std_dev = standard_deviation * np.sqrt(trading_days)
annual_std_dev.sort_values()

daily_returns.rolling(window=21).std().plot(figsize=(15, 7), title='Rolling 21-Day Standard Deviation', ylabel='Rolling 21-Day Std. Dev.')

daily_return_whale_funds.rolling(window=21).std().plot(figsize=(15, 7), title='Rolling 21-Day Standard Deviation', ylabel='Rolling 21-Day Std. Dev.')
```
The following plots are generated:
![image](https://user-images.githubusercontent.com/96163075/151417614-93f565e1-2cd3-4533-a1f1-a335586cb35e.png)
![image](https://user-images.githubusercontent.com/96163075/151417662-96a984b2-f7b8-4b1c-bf55-19a3d0a679a3.png)

Out of the four whale funds, Berkshire Hathaway poses the most risk since the rolling standard deviation is by far the greatest throughout the timeframe. However, between 2019 and 2020, Paulson & Co. Inc. posed more of a risk a few times throughout this period. The flash-crash of 2020 skews the data a bit, but over time, and after the flash-crash, Berkshire Hathaway still remians the highest risk due to the rolling standard deviation over time while the other three funds gradually returns back to their mean standard deviation.

---

### Part 4 - Analyzing the Risk-Return Profile














