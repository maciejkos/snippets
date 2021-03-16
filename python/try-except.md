#python #try #except #errors
 
```python

try:
	# do something
	pass

except ValueError:
	# handle ValueError exception
	pass

except (TypeError, ZeroDivisionError):
	# handle multiple exceptions
	# TypeError and ZeroDivisionError
	pass

except:
	# handle all other exceptions
	pass

else:
	# no exceptions, run this code

finally:
	# always run this code
	print("Cleaning up.")
	
# catch all exceptions and print
try:
	y = fun_y(x)
except Exception as e:
    print(f"Exception: {e}")

# raise your own exceptions
x = 10
if x > 5:
    raise Exception(f"x should not exceed 5. The value of x was:{x}")
```

References:
- https://www.programiz.com/python-programming/exception-handling
- https://realpython.com/python-exceptions/
- https://docs.python.org/3/tutorial/errors.html