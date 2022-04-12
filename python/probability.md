#python #itertools #probability

 
```python
# create all n element combinations and permutations of a list
import itertools

terms_ = ["a","b","c"]

n = 2

all_combinations_order_doesnt_matter = [sorted(list(x)) for x in itertools.combinations(terms_,n)]

all_permutations_order_matters = [sorted(list(x)) for x in itertools.permutations(terms_,n)]

print("all_combinations_order_doesnt_matter: ", all_combinations_order_doesnt_matter) # [['a', 'b'], ['a', 'c'], ['b', 'c']]
print("all_permutations_order_matters: ", all_permutations_order_matters) # [['a', 'b'], ['a', 'c'], ['a', 'b'], ['b', 'c'], ['a', 'c'], ['b', 'c']]


# get all permutations of two or more lists; full factorial design
treatment_a = ["a", "b"]
treatment_b = ["1", "2"]
treatment_c = ["X", "Y"]
treatments = [treatment_a, treatment_b, treatment_c]
list(itertools.product(*treatments))

# [('a', '1', 'X'),
#  ('a', '1', 'Y'),
#  ('a', '2', 'X'),
#  ('a', '2', 'Y'),
#  ('b', '1', 'X'),
#  ('b', '1', 'Y'),
#  ('b', '2', 'X'),
#  ('b', '2', 'Y')]

```