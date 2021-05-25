#unique #list #set #deepcopy

1. How to cast a list of list to a flat list? How to find unique elements in a list of lists?
2. How create a deep copy of a dict? 
```python
# 1. a list of lists to a set; unique elements in a list of lists
activities_schedule = [["walking"], ["walking"], ["walking", "talking"]]
set(activity for activities in activities_schedule for activity in activities)
# >>> {'talking', 'walking'}


# 2. make a deep copy of a dict
import copy
my_dict = {"a": 1, "b": 2}
my_deepcopy = copy.deepcopy(my_dict)

# 3. safely delete key from dict
my_dict.pop('key', None) # inplace, returns none if key doesn't exist

```