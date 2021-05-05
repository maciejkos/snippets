#unique #list #set #deepcopy
```python
# a list of lists to a set; unique elements in a list of lists
activities_schedule = [["walking"], ["walking"], ["walking", "talking"]]
# set(activity for activity in activities_schedule)
set(activity for activities in activities_schedule for activity in activities)
# >>> {'talking', 'walking'}


# make a deep copy of a dict
import copy
my_dict = {"a": 1, "b": 2}
my_deepcopy = copy.deepcopy(my_dict)
```