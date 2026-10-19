# otp.Source.uptick

#### ``Source.uptick(, discard_on_match=False, inplace=False)``

Propagates ticks based on its PRICE being strictly greater than that of the previous tick.

* **Parameters:**
  * **discard_on_match** (*bool*) – If this parameter is False (default), only ticks that match the filter will be propagated.
    Otherwise ticks that match the filter will be discarded.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Propagate only the ticks where field PRICE is greater than the PRICE of the previous tick:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE', 'EXCHANGE']]
>>> data = data.uptick()
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                            Time   PRICE  SIZE EXCHANGE
0  2024-02-01 04:00:00.011224206  185.50     2        K
1  2024-02-01 04:00:00.012928231  185.68    11        K
2  2024-02-01 04:00:00.012987210  185.72     5        K
3  2024-02-01 04:00:00.033759205  185.90    16        P
4  2024-02-01 04:00:00.169091123  185.90    87        P
..                           ...     ...   ...      ...
95 2024-02-01 04:12:37.454294671  185.87     1        P
96 2024-02-01 04:12:48.042468499  185.86     1        K
97 2024-02-01 04:13:15.728879547  185.86     3        Q
98 2024-02-01 04:13:26.821715886  185.84     2        K
99 2024-02-01 04:13:46.906139654  185.85    30        K
...
```

##### SEE ALSO
**UPTICK** OneTick event processor
