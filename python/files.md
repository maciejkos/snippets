```python

# list and filter files in a directory pathlib

import pathlib
path = pathlib.Path.cwd()

data_files = [file for file in path.iterdir() if "kos" in file.name and "zip" in file.suffix]

