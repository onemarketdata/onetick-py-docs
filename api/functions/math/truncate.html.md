# otp.math.truncate

### ``truncate(number, precision=0)``

Returns the `number` truncated to `precision` places right of the decimal point.

If `precision` is negative, the number is truncated to the left of the decimal point.

* **Parameters:**
  * **number** (float, ``decimal``, ``Operation``, ``Column``)
  * **precision** (int, ``Operation``, ``Column``)
* **Return type:**
  ``Operation``

#### NOTE
Truncating ``otp.nan`` returns NaN
and truncating ``otp.inf`` returns Infinity.

##### Examples

```
>>> data = otp.Ticks(A=[1.0, 1.23456, 123.456, 12345.6, otp.nan, otp.inf, -otp.inf])
>>> data['TRUNCATED'] = otp.math.truncate(data['A'])
>>> data['TRUNCATED_P2'] = otp.math.truncate(data['A'], 2)
>>> data['TRUNCATED_M2'] = otp.math.truncate(data['A'], -2)
>>> otp.run(data)
                     Time            A  TRUNCATED  TRUNCATED_P2  TRUNCATED_M2
0 2003-12-01 00:00:00.000      1.00000        1.0          1.00           0.0
1 2003-12-01 00:00:00.001      1.23456        1.0          1.23           0.0
2 2003-12-01 00:00:00.002    123.45600      123.0        123.45         100.0
3 2003-12-01 00:00:00.003  12345.60000    12345.0      12345.60       12300.0
4 2003-12-01 00:00:00.004          NaN        NaN           NaN           NaN
5 2003-12-01 00:00:00.005          inf        inf           inf           inf
6 2003-12-01 00:00:00.006         -inf       -inf          -inf          -inf
```

##### SEE ALSO
**TRUNCATE** OneTick function

