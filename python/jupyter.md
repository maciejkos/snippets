#print #colors #jupyter
```python

# How to print in colors in Jupyter?

colors = {"yellow" : '\033[93m',
          "green" : '\033[92m',
          "red" : '\033[91m',
          "blue" : '\033[94m',
          "pink" : '\033[95m',}       

for color_name, color_value in colors.items():
    print(f'{color_value} {color_name}')

```

![[Pasted image 20210505025445.png]] 

```shell
# How to convert ipynb to py
## !conda install -c defaults -c conda-forge ipynb-py-convert
## OR !pip install ipynb-py-convert
ipynb-py-convert examples/plot.ipynb examples/plot.py
```
