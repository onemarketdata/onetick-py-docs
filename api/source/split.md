# otp.Source.split

#### ``Source.split(expr, cases, default=False)``

The method splits data using passed expression `expr` for several
outputs by passed `cases`. The method is the alias for the ``Source.switch()``

* **Parameters:**
  * **expr** (*Operation*) – column or column based expression
  * **cases** (*list*) – list of values or ``onetick.py.range`` objects to split by
  * **default** (*bool*) – `True` adds the default output
  * **self** (*Source*)
* **Return type:**
  Outputs according to passed cases, number of outputs is number of cases plus one if `default=True`

##### Examples

```
>>> data = otp.Ticks(X=[0.33, -5.1, otp.nan, 9.4])
