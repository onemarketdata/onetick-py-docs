# otp.ops.ascii

### ``ascii(value)``

Returns the ASCII code of the first character in the string `value`.

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Get the ASCII code of the first character in the string literal:

```
>>> data = otp.Tick(A=otp.ops.ascii('hello'))
>>> otp.run(data)
        Time    A
0 2003-12-01  104
```

Get the ASCII code of the first character in each string of the column:

```
>>> data = otp.Ticks(A=['hello', 'world'])
>>> data['ASCII'] = otp.ops.ascii(data['A'])
>>> otp.run(data)
                     Time      A  ASCII
0 2003-12-01 00:00:00.000  hello    104
1 2003-12-01 00:00:00.001  world    119
```

##### SEE ALSO
**ASCII** OneTick function

