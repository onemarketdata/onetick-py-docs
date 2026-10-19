# otp.Source.volume_limit

#### ``Source.volume_limit(max_volume, , propagate_tick_at_crossed_boundary=False, discard_on_match=False, inplace=False)``

Propagates ticks based on the comparison of their total trading volume (the sum of field SIZE)
to the value specified by the parameter `max_volume`.

* **Parameters:**
  * **max_volume** (*int* *or* *float*) – The number with maximum trading volume.
  * **propagate_tick_at_crossed_boundary** (*bool*) – If True, the last tick that crossed the `max_volume` will be propagated, otherwise not.
    Default is False.
  * **discard_on_match** (*bool*) – If this parameter is False (default), only ticks that match the filter will be propagated.
    Otherwise ticks that match the filter will be discarded.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Filter out ticks after the cumulative volume exceeds 10 000 shares:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE', 'EXCHANGE']]
>>> data = data.volume_limit(10_000)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                             Time   PRICE  SIZE EXCHANGE
0   2024-02-01 04:00:00.008283417  186.50     6        K
1   2024-02-01 04:00:00.008290927  185.59     1        K
2   2024-02-01 04:00:00.008291153  185.49   107        K
3   2024-02-01 04:00:00.010381671  185.49     1        K
4   2024-02-01 04:00:00.011224206  185.50     2        K
..                            ...     ...   ...      ...
414 2024-02-01 04:20:20.380578855  185.80    50        K
415 2024-02-01 04:20:20.380599543  185.82    10        Q
416 2024-02-01 04:20:20.380601983  185.81     1        Q
417 2024-02-01 04:20:20.380604453  185.80    10        Q
418 2024-02-01 04:20:20.380609048  185.79    10        Q
...
```

Setting parameter `propagate_tick_at_crossed_boundary` will also propagate the tick that crossed the volume limit:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE', 'EXCHANGE']]
>>> data = data.volume_limit(10_000, propagate_tick_at_crossed_boundary=True)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                             Time   PRICE  SIZE EXCHANGE
0   2024-02-01 04:00:00.008283417  186.50     6        K
1   2024-02-01 04:00:00.008290927  185.59     1        K
2   2024-02-01 04:00:00.008291153  185.49   107        K
3   2024-02-01 04:00:00.010381671  185.49     1        K
4   2024-02-01 04:00:00.011224206  185.50     2        K
..                            ...     ...   ...      ...
415 2024-02-01 04:20:20.380599543  185.82    10        Q
416 2024-02-01 04:20:20.380601983  185.81     1        Q
417 2024-02-01 04:20:20.380604453  185.80    10        Q
418 2024-02-01 04:20:20.380609048  185.79    10        Q
419 2024-02-01 04:20:20.380611535  185.79    70        Q
...
```

##### SEE ALSO
**VOLUME_LIMIT** OneTick event processor
