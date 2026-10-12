# otp.math.degrees

### ``degrees(value)``

Returns the corresponding angle, in degrees, for `value` specified in radians.

* **Parameters:**
  **value** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['DEGREES'] = otp.math.degrees(otp.math.pi() / 4)  # should return 45
>>> otp.run(data)
        Time  A  DEGREES
0 2003-12-01  1     45.0
```

##### SEE ALSO
**DEGREES** OneTick function

``radians()``

