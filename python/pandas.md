#python #pandas 

```python
import pandas as pd

# subset pandas df by datetime range
def subset_by_dt_range(df, start: dt.datetime, end: dt.datetime, date_col_name: str = "datetime"):

    "Returns a subset of the dataframe that is within the given date range. Start and end are inclusive."

    return df[(df[date_col_name] >= start) & (df[date_col_name] <= end)]


# keep rows that don't contain a string #filter 
filter_str = "banned_word"
df.loc[~df.model.str.contains(filter_str): ]

# increase column width
pd.set_option("max_colwidth", 150)

# group / ungroup
## input
census_county_code = ["a", "b", "c", "d", "e", "f"] 
state_name = ["Utah"]*3 + ["Ohio"]*3
county_population = [1,2,3,11,12,13]
population_by_state = pd.DataFrame()
population_by_state["county"] = census_county_code
population_by_state["county_population"] = county_population
population_by_state["state"] = state_name
|    | county   |   county_population | state   |
|---:|:---------|--------------------:|:--------|
|  0 | a        |                   1 | Utah    |
|  1 | b        |                   2 | Utah    |
|  2 | c        |                   3 | Utah    |
|  3 | d        |                  11 | Ohio    |
|  4 | e        |                  12 | Ohio    |
|  5 | f        |                  13 | Ohio    |

## output
## I want to replace county_population with state_population, where state_population is a sum of county_population by state. It should look like this:


|    | county   |   state\_population  | state   |  
|---:|:---------|--------------------:|:--------|  
|  0 | a        |                   6 | Utah    |  
|  1 | b        |                   6 | Utah    |  
|  2 | c        |                   6 | Utah    |  
|  3 | d        |                  36 | Ohio    |  
|  4 | e        |                  36 | Ohio    |  
|  5 | f        |                  36 | Ohio    |

## this doesn't work: population\_by\_state.groupby(\["state"\])\[\["county\_population"\]\].sum().reset\_index().rename(columns={"county\_population":"state\_population"})

## solution

df.merge(df.set_index(['state', 'county'])['county_population'].sum(level='state').rename('state_population').reset_index()).drop(columns=['county_population']) # thanks, @smccabe!

## how to pretty print a dataframe
# first, you might need to 'conda install -c anaconda tabulate'

print(df.to_markdown(tablefmt="grid"))

## How to find unique combinations of values in n columns

def find_unique_combinations_of_column_values(df, cols):
    """
    Summary:
        Returns a list unique combinations of values from two columns in a dataframe
    Args:
        df (pandas.DataFrame): dataframe to search
        cols (list): list of columns to search
    Returns:
        a list of unique combinations of values from two columns in a dataframe
    
    Example:
        >>> df = pd.DataFrame({'A': [1, 2], 'B': [5, 6, 7, 8]})
        >>> unique_combinations(df, ['A', 'B'])
                                               
    """

    unique_combinations = df[cols].apply(lambda x: '_'.join(x.astype(str)), axis=1).unique()
    unique_combinations = [x for x in unique_combinations]
    return df[cols].apply(lambda x: '_'.join(x.astype(str)), axis=1).unique()
	
## How to transfrom columns from long to wide?

df = pd.DataFrame({
    'time': [1, 2, 1, 2],
    'metric_name': ["speed", "speed", "distance", "distance"],
    'metric_value': [15, 30, 5, 10]}).sort_values("time")
df

| time | metric_name | metric_value |
| :--- | :---------- | :----------- |
| 1    | speed       | 15           |
| 1    | distance    | 5            |
| 2    | speed       | 30           |
| 2    | distance    | 10           |


df_pivoted = (df.pivot_table(
    index=["time"], 
    columns=["metric_name"], 
    values="metric_value")
    ).rename_axis(None, axis=1).reset_index()
df_pivoted

| time | distance | speed |
| :--- | :------- | :---- |
| 1    | 5        | 15    |
| 2    | 10       | 30    |

## How to copy a dataframe as markdown to clipboard?
pd.io.clipboards.to_clipboard(df.to_markdown(), excel=False)

## How to increment value in column based on changes in value of another column?
# https://stackoverflow.com/a/47493345

|    | name_y   |     -——>     |    | name_y   |   name_group |
|---:|:---------|     -——>     |---:|:---------|-------------:|
|  0 | cat      |     -——>     |  0 | cat      |            1 |
|  1 | cat      |     -——>     |  1 | cat      |            1 |
|  2 | RATS!    |     -——>     |  2 | RATS!    |            2 |
|  3 | RATS!    |     -——>     |  3 | RATS!    |            2 |
|  4 | RATS!    |     -——>     |  4 | RATS!    |            2 |
|  5 | cat      |     -——>     |  5 | cat      |            3 |
|  6 | RATS!    |     -——>     |  6 | RATS!    |            4 |
|  7 | nan      |     -——>     |  7 | nan      |            5 |
|  8 | nan      |     -——>     |  8 | nan      |            5 |

df = pd.DataFrame()
df["name_y"] = pd.Series(["cat","cat","RATS!","RATS!","RATS!","cat","RATS!","nan","nan"])

import numpy as np
from itertools import groupby
grouped = [list(g) for k, g in groupby(df.name_y.tolist())]

name_group = np.repeat(range(len(grouped)),[len(x) for x in grouped])+1
df["name_group"] = name_group



```