#security #hash #sha256 

1. How create a sha256 hash of a string with salt?
```python

import hashlib
import secrets

text = "some text"
hash_name = "sha256"
# salt = "salty_salt_123" # a constant if you need to it for testing
salt = secrets.token_hex() # use this in prod; you might need to store the salt somewhere
salted_input_string = salt+text
hashed = hashlib.sha256(salted_input_string.encode('utf-8')).hexdigest()

```