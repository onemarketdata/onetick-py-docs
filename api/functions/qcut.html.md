# otp.qcut

### ``qcut(column, q, labels=None)``

Quantile-based discretization function (mimics `pandas.qcut`).

* **Parameters:**
  * **column** (``Column``) – Column with numeric data used to build bins.
  * **q** (*int* *or* *list* **[*float* *]*) – 

    When list[float] - array of quantiles, e.g. [0, .25, .5, .75, 1.] for quartiles.

    When int - Number of quantiles. 10 for deciles, 4 for quartiles, etc.
  * **labels** (*list* **[*str* *]*) – Labels used to name resulting bins.
    If not set, bins are numeric intervals like (5.0000000000, 7.5000000000].
* **Return type:**
  object that can be set to ``Column`` via ``__setitem__()``

##### Examples

```
>>> data = otp.Ticks({'X': [10, 3, 5, 6, 7, 1]})
>>> data['BIN'] = otp.qcut(data['X'], q=3, labels=['a', 'b', 'c'])
>>> otp.run(data)
                     Time   X BIN
0 2003-12-01 00:00:00.000  10   c
1 2003-12-01 00:00:00.001   3   a
2 2003-12-01 00:00:00.002   5   b
3 2003-12-01 00:00:00.003   6   b
4 2003-12-01 00:00:00.004   7   c
5 2003-12-01 00:00:00.005   1   a
```
