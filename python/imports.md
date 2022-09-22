#imports #python #modules
1. How to import a module from another directory?
2. How to reload an imported module?

```python
# 1. 
# Method a, which doesn't involve touching your system path
import importlib

path_testing_utils_py_file = path_project_root / "src" / "utils" / "testing_utils.py"

spec = importlib.util.spec_from_file_location(
  "t_utils", path_testing_utils_py_file)   
t_utils = importlib.util.module_from_spec(spec)       
spec.loader.exec_module(t_utils) # imported as t_utils

# Method b, which involves touching your system path
import sys

path_testing_utils_directory_with_module = path_project_root / "src" / "utils"
path_to_directory_with_module = path.parent.parent.absolute()
sys.path.insert(0, str(path_to_directory_with_module)) # now you can import the module using `import your_module as module_alias`

# 2. How to reload an imported module?

## Imagine you imported a module like this:
## import questions_utils as q_utils

## You made a change to the module and want to reload it without restarting the interpreter or kernel.

import importlib
importlib.reload(q_utils) # module is now reloaded
```