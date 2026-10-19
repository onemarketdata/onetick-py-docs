# otp.Source.interpolate

#### ``Source.interpolate(interval, fields, method='linear', , inplace=False)``

Compute a series of interpolated ticks at regular intervals.

* **Parameters:**
  * **method** (*str*) – When set to `linear` (default), linear interpolation is performed.
    When set to `step`, the last non-null value is taken as the interpolation result.
  * **interval** (*int*) – The interval in seconds to interpolate.
  * **fields** (*str* *or* *list* *or* *dict*) – A field name or a list of field names to interpolate, same field names are used in the output.
    If dictionary is passed, it is treated as mapping from input to output field names.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing. Otherwise method returns a new modified
    object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

10-second linear interpolation of *ASK_PRICE* and *BID_PRICE*:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> data = data.interpolate(10, ['ASK_PRICE', 'BID_PRICE'])
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                  Time   ASK_PRICE   BID_PRICE
0  2024-02-01 03:59:10   30.970272   30.614235
1  2024-02-01 03:59:20   62.177721   61.462920
2  2024-02-01 03:59:30   93.385170   92.311605
3  2024-02-01 03:59:40  124.592619  123.160290
4  2024-02-01 03:59:50  155.800068  154.008975
..                 ...         ...         ...
```

Use dictionary as `fields` parameter to specify output field names:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> data = data.interpolate(10, {'ASK_PRICE': 'ASK', 'BID_PRICE': 'BID'})
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                  Time         ASK         BID
0  2024-02-01 03:59:10   30.970272   30.614235
1  2024-02-01 03:59:20   62.177721   61.462920
2  2024-02-01 03:59:30   93.385170   92.311605
3  2024-02-01 03:59:40  124.592619  123.160290
4  2024-02-01 03:59:50  155.800068  154.008975
..                 ...         ...         ...
```

##### SEE ALSO
**INTERPOLATE** OneTick event processor
