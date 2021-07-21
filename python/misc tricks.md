#python 
1. How to get the name of a variable as string?
2. 
```python

# How to get the name of a variable as string?
import inspect

def retrieve_name(var):
	"""
	Returns the name of variable, not its value.
	Credit: https://stackoverflow.com/a/18425523
	"""
	callers_local_vars = inspect.currentframe().f_back.f_locals.items()
	return [var_name for var_name, var_val in callers_local_vars if var_val is var][0]
	
```