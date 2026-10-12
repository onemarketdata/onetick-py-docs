# otp.Operation.float.to_32nds

#### \_FloatAccessor.to_32nds(, throw_if_not_convertible=True)

Converts double number to *32nds* format string.

If `throw_if_not_convertible` flag is set to True (default),
function will throw an exception if it can not convert double to a *32nds* string,
otherwise it will return a string whose double implementation is close to the given number.

* **Parameters:**
  **throw_if_not_convertible** (bool or ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Convert double number to *32nds* format:

```
>>> data = otp.Ticks(PRICE=[100.0, 101 + 1/32, 102 + 16/32, 103 + 16.5/32, 104 + 7/256])
>>> data['PRICE_32NDS'] = data['PRICE'].float.to_32nds()
>>> otp.run(data)
                     Time       PRICE  PRICE_32NDS
0 2003-12-01 00:00:00.000  100.000000       100-00
1 2003-12-01 00:00:00.001  101.031250       101-01
2 2003-12-01 00:00:00.002  102.500000       102-16
3 2003-12-01 00:00:00.003  103.515625      103-16+
4 2003-12-01 00:00:00.004  104.027344      104-007
```

If the number can’t be converted, exception will be raised:

```
>>> data = otp.Ticks(PRICE=[100.0 + 1/33])
>>> data['PRICE_32NDS'] = data['PRICE'].float.to_32nds()
>>> otp.run(data)
Traceback (most recent call last):
Exception...Can't convert double to 32nds format string...
```

In this case parameter `throw_if_not_convertible=False` can be set,
and unconvertible values will be converted to the closest *32nds* value:

```
>>> data = otp.Ticks(PRICE=[100.0 + 1/33])
>>> data['PRICE_32NDS'] = data['PRICE'].float.to_32nds(throw_if_not_convertible=False)
>>> otp.run(data)
        Time       PRICE PRICE_32NDS
0 2003-12-01  100.030303     100-007
```

##### SEE ALSO
**CONVERT_DOUBLE_TO_32NDS** OneTick function

``from_32nds()``

