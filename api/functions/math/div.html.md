# otp.math.div

### ``div(value1, value2)``

Computes the quotient by dividing `value1` by `value2`.

* **Parameters:**
  * **value1** (int, float, ``decimal``, ``Operation``, ``Column``)
  * **value2** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=100, B=72)
>>> data['DIV'] = otp.math.div(data['A'], data['B'])
>>> otp.run(data)
        Time    A   B  DIV
0 2003-12-01  100  72    1
```

##### SEE ALSO
**DIV** OneTick function

mod

