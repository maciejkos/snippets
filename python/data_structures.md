#unique #list #set
```python
# a list of lists to a set; unique elements in a list of lists
activities_schedule = [["walking"], ["walking"], ["walking", "talking"]]
# set(activity for activity in activities_schedule)
set(activity for activities in activities_schedule for activity in activities)
# >>> {'talking', 'walking'}
```