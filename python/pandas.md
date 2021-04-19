#python #pandas 

```python
import pandas as pd

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


```