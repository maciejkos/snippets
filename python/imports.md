```python
import sys

path_to_directory_with_module = path.parent.parent.absolute()
sys.path.insert(0, str(path_to_directory_with_module))
```