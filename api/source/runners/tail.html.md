# otp.Source.tail (jupyter)

#### ``Source.tail(n=5, **kwargs)``

*Executes the query* and returns last `n` ticks as a pandas dataframe.

It is useful in the Jupyter case when you want to observe last `n` values.

* **Parameters:**
  * **n** (*int*) – number of ticks to return
  * **kwargs** – parameters will be passed to ``otp.run``
  * **self** (*Source*)
* **Return type:**
  `DataFrame`

##### Examples

```
>>> data = otp.Ticks(X=list('abcdefgik'))
>>> data.tail()
                     Time  X
0 2003-12-01 00:00:00.004  e
1 2003-12-01 00:00:00.005  f
2 2003-12-01 00:00:00.006  g
3 2003-12-01 00:00:00.007  i
4 2003-12-01 00:00:00.008  k
```

##### SEE ALSO
``onetick.py.agg.last()``

``otp.run``

``onetick.py.Source.head()``

``onetick.py.Source.count()``

