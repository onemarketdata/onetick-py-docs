# otp.Source.print_otq

#### ``Source.print_otq(**kwargs)``

Generate temporary .otq file with ``onetick.py.Source.to_otq()`` method,
print it to the standard output, then remove the file.

* **Parameters:**
  **kwargs** – Key-value arguments that are passed directly to ``onetick.py.Source.to_otq()``.

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data.print_otq()  
