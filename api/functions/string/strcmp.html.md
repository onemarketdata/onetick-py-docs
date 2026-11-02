# otp.ops.strcmp

### ``strcmp(value1, value2)``

Compares the strings `value1` and `value2`.
Returns 0 if they are equal, -1 if `value1` is lexicographically smaller than `value2`, 1 otherwise.

* **Parameters:**
  * **value1** (str, ``Operation``)
  * **value2** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Comparing string literals:

```
>>> data = otp.Tick(A=otp.ops.strcmp('hello', 'world'))
>>> otp.run(data)
        Time   A
0 2003-12-01  -1
```

Comparing each string in a column:

```
>>> data = otp.Ticks(A=['a', 'b', 'c'], B=['c', 'b', 'a'])
>>> data['X'] = otp.ops.strcmp(data['A'], data['B'])
>>> otp.run(data)
                     Time  A  B  X
0 2003-12-01 00:00:00.000  a  c -1
1 2003-12-01 00:00:00.001  b  b  0
2 2003-12-01 00:00:00.002  c  a  1
```

##### SEE ALSO
**STRCMP** OneTick function

