# onetick.py.Operation._\_ge_\_

#### Operation.\_\_ge_\_(other)

Return >= in filter operation.

##### Examples

```
>>> t = otp.Ticks(A=[0, 1, 2, 3])
>>> t = t.where(t['A'] >= 2)
>>> otp.run(t)
                     Time  A
0 2003-12-01 00:00:00.002  2
1 2003-12-01 00:00:00.003  3
```
