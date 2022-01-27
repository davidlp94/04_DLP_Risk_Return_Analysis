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

