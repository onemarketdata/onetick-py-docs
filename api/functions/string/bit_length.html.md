# otp.ops.bit_length

### ``bit_length(value)``

Returns the length of the string `value` in bits.

(If a byte with the value of 0 is present in the string, its position (0-based) multiplied by 8 is returned)

* **Parameters:**
  **value** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Get the length of a string literal in bits:

```
>>> data = otp.Tick(A=otp.ops.bit_length('hello'))
>>> otp.run(data)
        Time   A
0 2003-12-01  40
```

Get the length of each string in a column:

```
>>> data = otp.Ticks(A=['hello', 'world!'])
>>> data['BIT_LENGTH'] = otp.ops.bit_length(data['A'])
>>> otp.run(data)
                     Time       A  BIT_LENGTH
0 2003-12-01 00:00:00.000   hello          40
1 2003-12-01 00:00:00.001  world!          48
```

##### SEE ALSO
**BIT_LENGTH** OneTick function

