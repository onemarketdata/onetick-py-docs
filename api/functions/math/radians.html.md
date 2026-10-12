# otp.math.radians

### ``radians(value)``

Returns the corresponding angle, in radians, for `value` specified in degrees.

* **Parameters:**
  **value** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['RADIANS'] = otp.math.radians(45).round(4)  # should return pi/4 ~ 0.7854
>>> otp.run(data)
        Time  A  RADIANS
0 2003-12-01  1   0.7854
```

##### SEE ALSO
**RADIANS** OneTick function

``degrees()``

