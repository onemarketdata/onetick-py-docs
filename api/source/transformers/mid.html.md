# otp.Source.mid

#### ``Source.mid(output_field_name='MID', , inplace=False)``

Adds to the stream of quote ticks a numeric attribute
whose value for each tick is equal to the mid-quote: `MID = (BID_PRICE + ASK_PRICE) / 2`.

* **Parameters:**
  * **output_field_name** (*str*) – The name of the output field.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing. Otherwise method returns a new modified
    object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Add field **MID** to the output:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> data = data[['ASK_PRICE', 'BID_PRICE']]
>>> data = data.mid()
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                            Time  ASK_PRICE  BID_PRICE      MID
0  2024-02-01 03:59:00.048766251       0.00       0.00    0.000
1  2024-02-01 03:59:00.076961302       0.00       0.00    0.000
2  2024-02-01 04:00:00.004396668     187.02     184.87  185.945
3  2024-02-01 04:00:00.004557945     187.02     184.87  185.945
4  2024-02-01 04:00:00.004697438     187.02     184.87  185.945
..                           ...        ...        ...      ...
```

Parameter `output_field_name` can be used to change the name of the output field:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> data = data[['ASK_PRICE', 'BID_PRICE']]
>>> data = data.mid('MID_PRICE')
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                            Time  ASK_PRICE  BID_PRICE  MID_PRICE
0  2024-02-01 03:59:00.048766251       0.00       0.00      0.000
1  2024-02-01 03:59:00.076961302       0.00       0.00      0.000
2  2024-02-01 04:00:00.004396668     187.02     184.87    185.945
3  2024-02-01 04:00:00.004557945     187.02     184.87    185.945
4  2024-02-01 04:00:00.004697438     187.02     184.87    185.945
..                           ...        ...        ...        ...
```

##### SEE ALSO
**MID** OneTick event processor
