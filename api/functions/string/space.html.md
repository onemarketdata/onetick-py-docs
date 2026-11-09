# otp.ops.space

### ``space(count)``

Returns a string consisting of `count` spaces.

* **Parameters:**
  **count** (int, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Specify number of spaces as an integer:

```
>>> data = otp.Tick(A=otp.ops.space(10) + '!')
>>> otp.run(data)
        Time            A
0 2003-12-01            !
```

Get the number of spaces from a column:

```
>>> data = otp.Ticks(A=[1, 2, 3, 4, 5])
>>> data['X'] = '|' + otp.ops.space(data['A']) + '|'
>>> otp.run(data)
                     Time  A        X
0 2003-12-01 00:00:00.000  1      | |
1 2003-12-01 00:00:00.001  2     |  |
2 2003-12-01 00:00:00.002  3    |   |
3 2003-12-01 00:00:00.003  4   |    |
4 2003-12-01 00:00:00.004  5  |     |
```

##### SEE ALSO
**SPACE** OneTick function

