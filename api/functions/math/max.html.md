# otp.math.max

### ``max(*objs)``

Returns maximum value from list of `objs`.
The objects must be of the same type.

* **Parameters:**
  **objs** (int, float, ``decimal``, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['MAX'] = otp.math.max(5, data['A'])
>>> otp.run(data)
        Time  A  MAX
0 2003-12-01  1    5
```

##### SEE ALSO
**MAX** OneTick function

