# otp.math.gcd

### ``gcd(value1, value2)``

Computes the greatest common divisor between `value1` and `value2`.

* **Parameters:**
  * **value1** (int, float, ``decimal``, ``Operation``, ``Column``)
  * **value2** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=99, B=72)
>>> data['GCD'] = otp.math.gcd(data['A'], data['B'])
>>> otp.run(data)
        Time   A   B  GCD
0 2003-12-01  99  72    9
```

##### SEE ALSO
**GCD** OneTick function

