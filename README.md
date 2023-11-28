# Softwarepirate
Sea Level Predictor
# This Python 3 environment comes with many helpful analytics libraries installed
# For example, here's several helpful packages to load

import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 5GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
/kaggle/input/epa-sea-level.csv
You will anaylize a dataset of the global average sea level change since 1880. You will use the data to predict the sea level change through year 2050.
Load data
df = pd.read_csv('/kaggle/input/epa-sea-level.csv')
Create scatter plot
df.plot.scatter(x='Year', y="CSIRO Adjusted Sea Level", figsize=(25, 10))
sr1 = pd.Series([int(i) for i in range(1880, 2050)])

# First best line
slope, intercept, r_value, p_value, std_err  = linregress(df['Year'], df["CSIRO Adjusted Sea Level"])
plt.plot(sr1, intercept + slope*sr1, 'r', label='best fit line from 1880 to 2050')

# Second best line after year 2000
recent = df[df['Year'] >= 2000]
slope, intercept, r_value, p_value, std_err  = linregress(recent['Year'], recent["CSIRO Adjusted Sea Level"])

sr2 = pd.Series([int(i) for i in range(2000, 2050)])
recent.append(sr2, ignore_index=True)
plt.plot(sr2, intercept + slope*sr2, 'r', label='new best fit line after year 2000', color="pink")

plt.title("Rise in Sea Level")
plt.xlabel("Year")
plt.ylabel("Sea Level (inches)")
plt.legend()

plt.show()

 ![IMG_5777](https://github.com/Denjicode/Softwarepirate/assets/101855853/f998d176-2f75-45e9-8d8c-a64425cdacb3)
