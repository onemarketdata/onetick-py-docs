# otp.math.atn2

### ``atn2(y, x)``

Returns the principal value of inverse trigonometric function `arctan` of `y/x`.

* **Parameters:**
  * **y** (int, float, ``decimal``, ``Operation``, ``Column``)
  * **x** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['ATN2'] = otp.math.atn2(1, 1).round(4)  # should return pi/4 ~ 0.7854
>>> otp.run(data)
        Time  A    ATN2
0 2003-12-01  1  0.7854
```

##### SEE ALSO
**ATN2** OneTick function

