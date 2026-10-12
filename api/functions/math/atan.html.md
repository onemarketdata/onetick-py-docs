# otp.math.atan

### ``atan(value)``

Returns the value of inverse trigonometric function arctan.

* **Parameters:**
  **value** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['ATAN'] = otp.math.atan(1).round(4)  # should return pi/4 ~ 0.7854
>>> otp.run(data)
        Time  A    ATAN
0 2003-12-01  1  0.7854
```

`otp.math.arctan()` is the alias for ``atan()``:

```
>>> data = otp.Tick(A=1)
>>> data['ATAN'] = otp.math.arctan(1).round(4)
>>> otp.run(data)
        Time  A    ATAN
0 2003-12-01  1  0.7854
```

##### SEE ALSO
**ATAN** OneTick function

``onetick.py.math.pi()``

``onetick.py.math.tan()``

