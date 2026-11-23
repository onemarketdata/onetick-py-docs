# otp.ops.tick_byte_sum

### ``tick_byte_sum()``

Returns the sum of bytes across all fields of the tick.

This function is useful when comparing ticks that consist of multiple fields.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=[1, 2])
>>> data['TICK_BYTE_SUM'] = otp.ops.tick_byte_sum()
>>> otp.run(data)
                     Time  A  TICK_BYTE_SUM
0 2003-12-01 00:00:00.000  1              1
1 2003-12-01 00:00:00.001  2              2
```

```
>>> data = otp.Ticks(A=[1, 2], B=['hello', 'world'])
>>> data['TICK_BYTE_SUM'] = otp.ops.tick_byte_sum()
>>> otp.run(data)
                     Time  A      B  TICK_BYTE_SUM
0 2003-12-01 00:00:00.000  1  hello            533
1 2003-12-01 00:00:00.001  2  world            554
```

##### SEE ALSO
**TICK_BYTE_SUM** OneTick function

