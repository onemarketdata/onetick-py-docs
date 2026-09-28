# otp.cut

### ``cut(column, bins, labels=None)``

Bin values into discrete intervals (mimics `pandas.cut`).

* **Parameters:**
  * **column** (``Column``) – Column with numeric data used to build bins.
  * **bins** (*int* *or* *list* **[*float* *]*) – 

    When list[float] - defines the bin edges.

    When int - Defines the number of equal-width bins in the range of x.
  * **labels** (*list* **[*str* *]*) – Labels used to name resulting bins.
    If not set, bins are numeric intervals like (5.0000000000, 7.5000000000].
* **Return type:**
  object that can be set to ``Column`` via ``__setitem__()``

##### Examples

```
>>> data = otp.Ticks({'X': [9, 8, 5, 6, 7, 0, ]})
>>> data['BIN'] = otp.cut(data['X'], bins=3, labels=['a', 'b', 'c'])
>>> otp.run(data)
                     Time  X BIN
0 2003-12-01 00:00:00.000  9   c
1 2003-12-01 00:00:00.001  8   c
2 2003-12-01 00:00:00.002  5   b
3 2003-12-01 00:00:00.003  6   b
4 2003-12-01 00:00:00.004  7   c
5 2003-12-01 00:00:00.005  0   a
```
