# otp.Operation.str.from_32nds

#### \_StrAccessor.from_32nds(, throw_if_not_convertible=True)

Converts *32nds* format string to double.

If `throw_if_not_convertible` flag is set to True (default),
the function will throw an exception on error,
otherwise it will return NaN.

* **Parameters:**
  **throw_if_not_convertible** (bool or ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Convert to *32nds* format strings to double numbers:

```
>>> data = otp.Ticks(PRICE_32NDS=['100-00', '101-01', '102-16', '103-16+', '104-007'])
>>> data['PRICE'] = data['PRICE_32NDS'].str.from_32nds()
>>> otp.run(data)
                     Time PRICE_32NDS       PRICE
0 2003-12-01 00:00:00.000      100-00  100.000000
1 2003-12-01 00:00:00.001      101-01  101.031250
2 2003-12-01 00:00:00.002      102-16  102.500000
3 2003-12-01 00:00:00.003     103-16+  103.515625
4 2003-12-01 00:00:00.004     104-007  104.027344
```

If the number can’t be converted, exception will be raised:

```
>>> data = otp.Ticks(PRICE_32NDS=['wrong'])
>>> data['PRICE'] = data['PRICE_32NDS'].str.from_32nds()
>>> otp.run(data)
Traceback (most recent call last):
Exception...String for conversion should be in NNN-nn[+] or NN-nn[+] format...
```

In this case parameter `throw_if_not_convertible=False` can be set,
and unconvertible values will be converted to NaN values:

```
>>> data = otp.Ticks(PRICE_32NDS=['wrong'])
>>> data['PRICE'] = data['PRICE_32NDS'].str.from_32nds(throw_if_not_convertible=False)
>>> otp.run(data)
        Time PRICE_32NDS  PRICE
0 2003-12-01       wrong    NaN
```

##### SEE ALSO
**CONVERT_32NDS_TO_DOUBLE** OneTick function

``to_32nds()``

