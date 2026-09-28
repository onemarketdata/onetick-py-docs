# onetick.py.Operation._\_mod_\_

#### Operation.\_\_mod_\_(other)

Return modulo of division of int column by `other` value.

* **Parameters:**
  **other** (int, ``onetick.py.Column``)

##### Examples

```
>>> t = otp.Tick(A=3, B=3)
>>> t['A'] = t['A'] % t['B']
>>> t['B'] = t['B'] % 2
>>> otp.run(t)
        Time  A  B
0 2003-12-01  0  1
```
