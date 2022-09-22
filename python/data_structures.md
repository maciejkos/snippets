#unique #list #set #deepcopy

1. How to cast a list of list to a flat list? How to find unique elements in a list of lists?
2. How create a deep copy of a dict? 
3. How to safely delete key from dict?
4. How to print keys or values of a nested dict
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

# 4. print keys or values of a nested dict
def get_keys_or_values_of_nested_dict(iterable, returned="key") -> Iterable:
    
    """
    Returns an iterator that returns all keys or values
       of a (nested) iterable. Useful for printing all keys of a nested dict when printing values is not desired (e.g., values are dataframes).
       
    Args:
        iterable (dict): iterable to get keys or values from
        returned (str): "key" or "value" to return
    
    Returns:
        Iterable: iterator that returns all keys or values
           
    Examples:
        people = {"Jim":{"tall": "yes", "last letter": "m"}, "Jack":{"tall": "yes", "last letter": "k"}, "Jane":{"tall": "yes", "last letter": "e"}, "Jill":{"tall": "yes", "last letter": "l"}}
        
        list(get_keys_or_values_of_iterable(people, returned="key"))
        → ['Jim', 'tall', 'last letter', 'Jack', 'tall', 'last letter', 'Jane', 'tall', 'last letter', 'Jill', 'tall', 'last letter']

        list(get_keys_or_values_of_iterable(people, returned="value"))
        → ['yes', 'm', 'yes', 'k', 'yes', 'e', 'yes', 'l']
    
    Source and author: 
        https://gist.github.com/PatrikHlobil/9d045e43fe44df2d5fd8b570f9fd78cc#file-nested_iterator-py
    """
  
    if isinstance(iterable, dict):
        for key, value in iterable.items():
            if returned == "key":
                yield key
            elif returned == "value":
                if not (isinstance(value, dict) or isinstance(value, list)):
                    yield value
            else:
                raise ValueError("'returned' keyword only accepts 'key' or 'value'.")
            for ret in get_keys_or_values_of_nested_dict(value, returned=returned):
                yield ret
    
    ## this part doesn't seem to work in the original code, which is linked to in the docstring
    # elif isinstance(iterable, list):
    #     for el in iterable:
    #         for ret in get_keys_or_values_of_nested_dict(el, returned=returned):
    #             yield ret

```