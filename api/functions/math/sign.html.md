# otp.math.sign

### ``sign(value)``

Compute the sign of the `value`.

* **Parameters:**
  **value** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=[123, 0, -123])
>>> data['SIGN'] = otp.math.sign(data['A'])
>>> otp.run(data)
                     Time    A  SIGN
0 2003-12-01 00:00:00.000  123     1
1 2003-12-01 00:00:00.001    0     0
2 2003-12-01 00:00:00.002 -123    -1
```

##### SEE ALSO
**SIGN** OneTick function

