```python
# timeit: https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-timeit

### How do I run timeit in line mode?
%timeit -r 8 -n 10 -p 7 True == False # print with precition of 7 digits; do 8 runs of `True == False`, each run is 10 loops; so in total, `True == False` is checked 80 times (r*n 8*10) 

## timeit line mode
### %timeit [-n<N> -r<R> [-t|-c] -q -p<P> -o] statement

## timeit cell mode
### %%timeit [-n<N> -r<R> [-t|-c] -q -p<P> -o] setup_code code code…



```