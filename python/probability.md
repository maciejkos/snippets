#python #itertools #probability

 
```python
# create all n element combinations and permutations of a list

terms_ = ["a","b","c"]

n = 2

all_combinations_order_doesnt_matter = [sorted(list(x)) for x in itertools.combinations(terms_,n)]

all_permutations_order_matters = [sorted(list(x)) for x in itertools.permutations(terms_,n)]

print("all_combinations_order_doesnt_matter: ", all_combinations_order_doesnt_matter) # [['a', 'b'], ['a', 'c'], ['b', 'c']]
print("all_permutations_order_matters: ", all_permutations_order_matters) # [['a', 'b'], ['a', 'c'], ['a', 'b'], ['b', 'c'], ['a', 'c'], ['b', 'c']]
```