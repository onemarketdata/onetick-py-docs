# otp.Source.intercept_initialization_ticks

#### ``Source.intercept_initialization_ticks(inplace=False)``

Removes initialization ticks (the ticks that arrived before the start time of the query),
thus preventing them from delivery to the client application.

* **Parameters:**
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Ticks taken from before the start time of the query
with `back_to_first_tick` parameter are initialization ticks
and can be seen with ``show_initialization_ticks()``:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL', date=otp.dt(2024, 2, 1),
...                       back_to_first_tick=otp.Day(1), max_back_ticks_to_prepend=100)
>>> data = data[['PRICE', 'SIZE']]
>>> data['TICK_TIME'] = data['TIMESTAMP']
>>> data = data.show_initialization_ticks()
>>> otp.run(data)
         Time     PRICE  SIZE                     TICK_TIME
0  2024-02-01  185.6800    10 2024-01-31 19:59:57.877747563
1  2024-02-01  185.6999     5 2024-01-31 19:59:53.314804162
2  2024-02-01  185.7000   100 2024-01-31 19:59:53.302285347
3  2024-02-01  185.6900     1 2024-01-31 19:59:53.019288051
4  2024-02-01  185.7000   440 2024-01-31 19:59:51.062739337
...
```

Intercepting initialization ticks will remove them from the data flow:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL', date=otp.dt(2024, 2, 1),
...                       back_to_first_tick=otp.Day(1), max_back_ticks_to_prepend=100)
>>> data = data[['PRICE', 'SIZE']]
>>> data['TICK_TIME'] = data['TIMESTAMP']
>>> data = data.intercept_initialization_ticks()
>>> data = data.show_initialization_ticks()
>>> otp.run(data)
Empty DataFrame
...
```

##### SEE ALSO
**INTERCEPT_INITIALIZATION_TICKS** OneTick event processor

``show_initialization_ticks()``

