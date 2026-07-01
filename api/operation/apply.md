# otp.Operation.apply

#### ``Operation.apply(lambda_f)``

Apply function or type to column

* **Parameters:**
  **lambda_f** (*type* *or* *callable*) – 

  if type - will convert column to requested type

  if callable - will translate python code to similar OneTick’s CASE expression.
  There are some limitations to which python operators can be used in this callable.
  See `Python callables parsing guide` article for details.
  In `Remote OTP with Ray` any Callable must be decorated with @otp.remote decorator,
  see `Ray usage examples` for details.

##### Examples

Converting type of the column, e.g. string column to integer:

```
>>> data = otp.Ticks({'A': ['1', '2', '3']})
>>> data['B'] = data['A'].apply(int) + 10
>>> otp.run(data)
