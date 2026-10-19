# otp.Source.add_fields_from_symbol_params

#### ``Source.add_fields_from_symbol_params(, prefix=None, inplace=False)``

Modifies the input time series by adding all symbol parameters
(preserving original value types) as new fields to each tick.

#### NOTE
This OneTick EP returns arbitrary number of fields,
so the source’s ``schema`` will not be updated automatically.

* **Parameters:**
  * **prefix** (*str*) – If specified, it will be appended to each added tick field name with the following form:
    `PREFIX.SYMBOL_PARAM_NAME`
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing. Otherwise method returns a new modified
    object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Let’s create first-stage query with some symbol parameters first:

```
>>> symbols = otp.Tick(SYMBOL_NAME='AAPL', PARAM_1='HELLO', PARAM_2=12345, PARAM_3=1.2345)
```

Then add these symbol parameters as new fields:

```
>>> data = otp.Tick(A=1)
>>> data = data.add_fields_from_symbol_params()
>>> data = otp.merge([data], symbols=symbols)
>>> otp.run(data)
        Time  A PARAM_1  PARAM_2  PARAM_3
0 2003-12-01  1   HELLO    12345   1.2345
```

Note that source’s ``schema`` can’t be updated automatically in this case
and need to be set manually in order to use new fields:

```
>>> data.schema.update(**{'PARAM_1': str, 'PARAM_2': int, 'PARAM_3': float})
>>> data['B'] = data['PARAM_2'] + 1
>>> otp.run(data)
        Time  A PARAM_1  PARAM_2  PARAM_3      B
0 2003-12-01  1   HELLO    12345   1.2345  12346
```

Parameter `prefix` can be used to add some prefix to the new fields:

```
>>> data = otp.Tick(A=1)
>>> data = data.add_fields_from_symbol_params(prefix='PREFIX')
>>> data = otp.merge([data], symbols=symbols)
>>> otp.run(data)
        Time  A PREFIX.PARAM_1  PREFIX.PARAM_2  PREFIX.PARAM_3
0 2003-12-01  1          HELLO           12345          1.2345
```

##### SEE ALSO
**ADD_FIELDS_FROM_SYMBOL_PARAMS** OneTick event processor
