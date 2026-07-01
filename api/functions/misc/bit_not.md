# otp.misc.bit_not

### ``bit_not(value)``

Performs the logical NOT operation on each bit of the `value`.

* **Parameters:**
  **value** (int, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

##### Examples

Basic example:

```
>>> data = otp.Tick(A=1)
>>> data['NOT'] = otp.bit_not(1)
>>> otp.run(data)
        Time  A  NOT
0 2003-12-01  1   -2
