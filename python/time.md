#python #time 
 
```python
# make date
dt.datetime(2017, 1, 1, 0, 0)

# make timestamp
pd.to_datetime(dt.datetime(2017, 1, 1, 0, 0))

# get date string
pd.to_datetime(dt.datetime(2017, 1, 1, 0, 0)).strftime('%Y %m')

# get date from string
pd.to_datetime('2023-05-27').strftime('%Y-%m-%d')

# parse dates
df = pd.read_csv(fp, dtype=str, parse_dates=['date'], index_col='date') 

# subset pandas df by datetime range
def subset_by_dt_range(df, start: dt.datetime, end: dt.datetime, date_col_name: str = "datetime"):

    "Returns a subset of the dataframe that is within the given date range. Start and end are inclusive."

    return df[(df[date_col_name] >= start) & (df[date_col_name] <= end)]

# decompose: multiplicative 
from statsmodels.tsa.seasonal import seasonal_decompose 
result_mul = seasonal_decompose(df['value'], model='multiplicative', extrapolate_trend='freq')
result_mul.plot().suptitle('Multiplicative Decompose', fontsize=22)

# decompose: additive
from statsmodels.tsa.seasonal import seasonal_decompose
result_add = seasonal_decompose(df['value'], model='additive', extrapolate_trend='freq')
result_add.plot().suptitle('Additive Decompose', fontsize=22)

# detrend: subtract the line of best fit
from scipy import signal
detrended_least_sq_fit = signal.detrend(df.signal.values)

# detrend: the Trend Component.
from statsmodels.tsa.seasonal import seasonal_decompose
result_mul = seasonal_decompose(df['signal'], model='multiplicative', extrapolate_trend='freq')
detrended_trend_comp = df.signal.values - result_mul.trend

# deseasonize
result_mul = seasonal_decompose(df['signal'], model='multiplicative', extrapolate_trend='freq')
deseasonalized = df.signal.values / result_mul.seasonal

# autocorrelation
from pandas.plotting import autocorrelation_plot
autocorrelation_plot(df.signal.tolist())
```