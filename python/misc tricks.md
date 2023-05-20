#python 
1. How to get the name of a variable as string?
2. How to capture what a function prints, save it to a file, while allowing the function to print in real-time? #context #manager
3. How to reload an imported module?
4. How do I get the size of an object with memory (with all references)?
```python

# 1. How to get the name of a variable as string?
import inspect

def retrieve_name(var):
	"""
	Returns the name of variable, not its value.
	Credit: https://stackoverflow.com/a/18425523
	"""
	callers_local_vars = inspect.currentframe().f_back.f_locals.items()
	return [var_name for var_name, var_val in callers_local_vars if var_val is var][0]
	
# 2. How to capture what a function prints, save it to a file, while allowing the function to print in real-time? 
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

# 3. How to reload an imported module?

## Imagine you imported a module like this:
## import questions_utils as q_utils

## You made a change to the module and want to reload it without restarting the interpreter or kernel.

import importlib
importlib.reload(q_utils) # module is now reloaded


# 4. How do I get the size of an object with memory (with all references)?

import sys
import gc
import math

def convert_size(size_bytes):
   """
   Source: https://stackoverflow.com/a/14822210
   """
   if size_bytes == 0:
       return "0B"
   size_name = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
   i = int(math.floor(math.log(size_bytes, 1024)))
   p = math.pow(1024, i)
   s = round(size_bytes / p, 2)
   return "%s %s" % (s, size_name[i])


def get_actual_size(input_obj):
    """
    Gets object size in bytes and converts it to human-readable form; works for nested objects and grabs all objects that are referenced by the input object

    Source: https://towardsdatascience.com/the-strange-size-of-python-objects-in-memory-ce87bdfbb97f  (with a single modification: added convert_size() on the last line)
    """
    memory_size = 0
    ids = set()
    objects = [input_obj]
    while objects:
        new = []
        for obj in objects:
            if id(obj) not in ids:
                ids.add(id(obj))
                memory_size += sys.getsizeof(obj)
                new.append(obj)
        objects = gc.get_referents(*new)
    return convert_size(memory_size)

get_actual_size(figures)
```
