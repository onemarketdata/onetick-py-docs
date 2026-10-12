# otp.math.exp

### ``exp(value)``

Compute the natural exponent of the `value`.

* **Parameters:**
  **value** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['E'] = otp.math.exp(1)
>>> otp.run(data)
        Time  A         E
0 2003-12-01  1  2.718282
```

##### SEE ALSO
**EXP** OneTick function

``onetick.py.math.ln()``

