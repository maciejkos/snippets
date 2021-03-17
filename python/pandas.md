#python #pandas 

```python
import pandas as pd

# keep rows that don't contain a string #filter 
filter_str = "banned_word"
df.loc[~df.model.str.contains(filter_str): ]

# increase column width
pd.set_option("max_colwidth", 150)

```