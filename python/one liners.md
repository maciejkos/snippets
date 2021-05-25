```python

s = "1-2-3"
list_of_strings = [a,b,c] = s.split("-") # ['1', '2', '3']; a = 1, etc.
list_of_strings = [s.split("-")] # the same as above but without assignment to a, b, c
list_of_ints = list(map(lambda x: int(x), s.split("-"))) # [1, 2, 3]
```
