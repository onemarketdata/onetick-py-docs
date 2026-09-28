# otp.Source.head (jupyter)

#### ``Source.head(n=5, **kwargs)``

*Executes the query* and returns first `n` ticks as a pandas dataframe.

It is useful in the Jupyter case when you want to observe first `n` values.

* **Parameters:**
  * **n** (*int* *,* *default=5*) – number of ticks to return
  * **kwargs** – parameters will be passed to ``otp.run``
  * **self** (*Source*)
* **Return type:**
  `DataFrame`

##### Examples

```
>>> data = otp.Ticks(X=list('abcdefgik'))
>>> data.head()
                     Time  X
0 2003-12-01 00:00:00.000  a
1 2003-12-01 00:00:00.001  b
2 2003-12-01 00:00:00.002  c
3 2003-12-01 00:00:00.003  d
4 2003-12-01 00:00:00.004  e
```

##### SEE ALSO
``onetick.py.agg.first()``

``otp.run``

``onetick.py.Source.tail()``

``onetick.py.Source.count()``

