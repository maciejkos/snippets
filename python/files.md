1. How to list and filter all files in a directory / folder?
2. How to convert a Jupyter Notebook (.ipynb) to a script (.py)

```python
# 1. list and filter files in a directory pathlib

import pathlib
path = pathlib.Path.cwd()

data_files = [file for file in path.iterdir() if "kos" in file.name and "zip" in file.suffix]

```


```python
# 2. Convert ipynb to py
jupyter nbconvert --to script [YOUR_NOTEBOOK].ipynb
```