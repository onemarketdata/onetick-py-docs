# onetick.py.Operation._\_rtruediv_\_

#### Operation.\_\_rtruediv_\_(other)

##### Examples

```
>>> t = otp.Tick(A=1, B=2.3)
>>> t['A'] /= t['B']
>>> t['B'] /= 2
>>> otp.run(t)
        Time         A     B
0 2003-12-01  0.434783  1.15
```

##### SEE ALSO
``__truediv__``
