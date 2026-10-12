# otp.math.mod

### ``mod(value1, value2)``

Computes the remainder from dividing `value1` by `value2`.

* **Parameters:**
  * **value1** (int, float, ``decimal``, ``Operation``, ``Column``)
  * **value2** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=100, B=72)
>>> data['MOD'] = otp.math.mod(data['A'], data['B'])
>>> otp.run(data)
        Time    A   B  MOD
0 2003-12-01  100  72   28
```

##### SEE ALSO
**MOD** OneTick function

div

