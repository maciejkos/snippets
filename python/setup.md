#python #setup #config 
 
```python
for_reqs = ['pandas' , 'matplotlib', 'seaborn==0.11.1', 'tqdm', 'plotly==4.14.3', 'pyjanitor', 'scipy', 'sklearn', 'statsmodels', 'plotnine']

requirements = [f'{requirement}\n' for requirement in for_reqs]

with open('requirements.txt', 'w') as fp:
    for line in requirements:
    	fp.write(line)

!pip install -r requirements.txt

import sys
import copy
from typing import List, Set, Dict, Tuple, Optional
import pathlib
from pprint import pprint
import numpy as np
import pandas as pd
import scipy.stats as stats
import statsmodels.api as sm
%matplotlib inline
from dateutil.parser import parse 
from matplotlib import pyplot as plt
import matplotlib.ticker as mtick
import seaborn as sns
import plotly.express as px
import plotly
import datetime as dt
from janitor import groupby_agg
from sklearn import svm
from tqdm.auto import tqdm
from plotnine import *
pd.set_option("max_colwidth", 150)
%precision 10

path = pathlib.Path.cwd()

plt.rcParams.update({'figure.figsize': (10,10)})
plt.rcParams['figure.dpi']= 300
%config InlineBackend.figure_format = 'svg'
pd.options.plotting.backend = 'plotly'
print('\nSetup done.')
```