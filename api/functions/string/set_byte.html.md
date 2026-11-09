# otp.ops.set_byte

### ``set_byte(value, index, byte_value)``

Returns a string with byte at position `index` (0-based) of string `value` changed to `byte_value`.

If `index` is outside of `value`’s boundaries, returned string is identical to `value`.

* **Parameters:**
  * **value** (str, ``Operation``)
  * **index** (int, ``Operation``)
  * **byte_value** (int, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Change byte in string literal:

```
>>> data = otp.Tick(A=otp.ops.set_byte('hello', 2, 88))
>>> otp.run(data)
        Time      A
0 2003-12-01  heXlo
```

Change byte for each string in a column:

```
>>> data = otp.Ticks(A=[0, 1, 2, 3, 4, 5])
>>> data['X'] = otp.ops.set_byte('hello', data['A'], 88)
>>> otp.run(data)
                     Time  A      X
0 2003-12-01 00:00:00.000  0  Xello
1 2003-12-01 00:00:00.001  1  hXllo
2 2003-12-01 00:00:00.002  2  heXlo
3 2003-12-01 00:00:00.003  3  helXo
4 2003-12-01 00:00:00.004  4  hellX
5 2003-12-01 00:00:00.005  5  hello
```

##### SEE ALSO
**SET_BYTE** OneTick function

