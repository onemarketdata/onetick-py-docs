# otp.Column.tick_shift

#### ``Column.tick_shift(offset, , , group_by=None)``

Returns the value of this column from a tick preceding the current one by `offset`.

Boundary values will be set to the default value by type: 0 for integers, empty string for strings, etc.

* **Parameters:**
  * **offset** (*int*) – Non negative offset looking back from the current tick.
  * **group_by** (*str* *|* *list* **[*str* *]*) – Specifies a field name or a list of field names,
    in which case `offset` is counted among the ticks with same values of the specified fields.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=[1, 2, 3, 4, 5, 6, 7, 8, 9], B=[1, 1, 1, 2, 2, 3, 3, 2, 3])
>>> data['A1'] = data['A'].tick_shift(1)
>>> data['A1_GROUP_BY_B'] = data['A'].tick_shift(1, group_by='B')
>>> otp.run(data)
                     Time  A  B  A1  A1_GROUP_BY_B
0 2003-12-01 00:00:00.000  1  1   0              0
1 2003-12-01 00:00:00.001  2  1   1              1
2 2003-12-01 00:00:00.002  3  1   2              2
3 2003-12-01 00:00:00.003  4  2   3              0
4 2003-12-01 00:00:00.004  5  2   4              4
5 2003-12-01 00:00:00.005  6  3   5              0
6 2003-12-01 00:00:00.006  7  3   6              6
7 2003-12-01 00:00:00.007  8  2   7              5
8 2003-12-01 00:00:00.008  9  3   8              7
```

##### SEE ALSO
``__getitem__()``

**TICK_SHIFT** OneTick function

