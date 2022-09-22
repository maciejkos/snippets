#python 
1. How to get the name of a variable as string?
2. How to capture what a function prints, save it to a file, while allowing the function to print in real-time? #context #manager
3. How to reload an imported module?
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
	
# How to capture what a function prints, save it to a file, while allowing the function to print in real-time? 
# Thanks Nathan Buckner!

from io import StringIO
from pathlib import Path
import sys

class Capturing:
    def __init__(self, path: Path = None, string_io: bool = False, overwrite_path: bool = True):
        if string_io:
            self.data = StringIO()
        if path:
            self.path = Path(path).expanduser().resolve()
            if overwrite_path:
                self.path.unlink()
    def write(self, string):
        if hasattr(self, "data"):
            self.data.write(string)
        if getattr(self, "path", None):
            with open(self.path, "a") as fp:
                fp.write(string)
        sys.__stdout__.write(string)
    def flush(self):
        sys.__stdout__.flush()
    def __enter__(self):
        sys.stdout = self
        return self
    def __exit__(self, *args):
        sys.stdout = sys.__stdout__
		
def test():
    print(1)
    print(2)
    print(3)
	
with Capturing("output") as capturing:
    test()
print(capturing.path)

with Capturing(string_io=True) as capturing:
    test()
print(capturing.data.getvalue())

# How to reload an imported module?

## Imagine you imported a module like this:
## import questions_utils as q_utils

## You made a change to the module and want to reload it without restarting the interpreter or kernel.

import importlib
importlib.reload(q_utils) # module is now reloaded

```
