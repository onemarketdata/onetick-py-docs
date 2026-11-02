# otp.ops.byte_at

### ``byte_at(value, index)``

Returns the integer byte value from the string `value` at the position indicated by the 0-based `index`.
Returns -1, if the byte does not exist on this position.

* **Parameters:**
  * **value** (str, ``Operation``)
  * **index** (int, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Get byte in string literal:

```
>>> data = otp.Tick(A=otp.ops.byte_at('hello', 1))
>>> otp.run(data)
        Time    A
0 2003-12-01  101
```

Get the byte for each letter in a string:

```
>>> data = otp.Ticks(A=[0, 1, 2, 3, 4, 5])
>>> data['X'] = otp.ops.byte_at('hello', data['A'])
>>> otp.run(data)
                     Time  A    X
0 2003-12-01 00:00:00.000  0  104
1 2003-12-01 00:00:00.001  1  101
2 2003-12-01 00:00:00.002  2  108
3 2003-12-01 00:00:00.003  3  108
4 2003-12-01 00:00:00.004  4  111
5 2003-12-01 00:00:00.005  5   -1
```

##### SEE ALSO
**BYTE_AT** OneTick function

