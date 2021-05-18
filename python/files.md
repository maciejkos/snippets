#zip #pathlib #ipynb

1. How to list and filter all files in a directory / folder?
2. How to convert a Jupyter Notebook (.ipynb) to a script (.py)
3. How to unzip a file?

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

```python
# 3. Unzip a file
# requires 7zip to be installed on the OS

from zipfile import ZipFile
import subprocess, sys
import pathlib

path = pathlib.Path.cwd()

zip_file = path / "some_archive.zip"
password = 'some_password'
destination_directory = path / "folder_storing_unzipped_files"

def unzip(zipFile_, destination_directory_, password_):
    try:
        with ZipFile(zipFile_, 'r') as zipObj:
            # Extract all the contents of zip file in different directory
            zipObj.extractall(destination_directory_)
    except:
        print("An exception occurred extracting with Python ZipFile library.")
        print("Attempting to extract using 7zip")

        unzip_process = subprocess.Popen(["7z", "e", f"{zipFile_}", f"-o{destination_directory_}", "-y", f"-p{password_}"], stdout=subprocess.PIPE, stderr=subprocess.PIPE)

    out, err = unzip_process.communicate()
	
    out = out.decode('UTF-8')
    err = err.decode('UTF-8')
	
    if err == "":
        print(f"Extracted: {zip_file}")
    else:
        print(f"ERROR with: {zip_file}")
        print(err)

unzip(zip_file, destination_directory,password)
```