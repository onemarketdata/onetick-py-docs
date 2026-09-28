# onetick.py.Operation._\_ne_\_

#### Operation.\_\_ne_\_(other)

Return inequality in filter operation.

##### Examples

```
>>> t = otp.Ticks(A=[0, 1, 2, 3])
>>> t = t.where(t['A'] != 1)
>>> otp.run(t)
                     Time  A
0 2003-12-01 00:00:00.000  0
1 2003-12-01 00:00:00.002  2
2 2003-12-01 00:00:00.003  3
```
