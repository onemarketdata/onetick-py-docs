# onetick.py.Operation._\_neg_\_

#### Operation.\_\_neg_\_()

Return the negative value of float or int column.

##### Examples

```
>>> t = otp.Tick(A=1, B=2.3)
>>> t['A'] = -t['A']
>>> t['B'] = -t['B']
>>> otp.run(t)
        Time   A     B
0 2003-12-01  -1  -2.3
```
