# otp.Source.byte_present

#### ``Source.byte_present(field, , bytes, , discard_on_match=False, inplace=False)``

Propagates ticks based on whether the value of the `field`
contains a byte in the set of `bytes`.

* **Parameters:**
  * **field** (str, ``Column``) – The name of the field to apply filter to.
  * **bytes** (*list*) – List of bytes values expressed as integers or strings or a comma-separated string.
    Both hexadecimal and decimal formats are supported.
    Note that invalid byte values are converted to zero.
  * **discard_on_match** (*bool*) – If this parameter is False (default), only ticks that match the filter will be propagated.
    Otherwise ticks that match the filter will be discarded.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Propagate only the ticks where field EXCHANGE contains P or Q characters
(expressed as ASCII decimal or hex values):

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE', 'EXCHANGE']]
>>> data = data.byte_present('EXCHANGE', [0x51, 80])
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                            Time   PRICE  SIZE EXCHANGE
0  2024-02-01 04:00:00.033759205  185.90    16        P
1  2024-02-01 04:00:00.169091123  185.90    87        P
2  2024-02-01 04:00:00.413581861  185.98     1        P
3  2024-02-01 04:00:00.721593975  185.77     6        P
4  2024-02-01 04:00:00.721594183  185.76     1        P
..                           ...     ...   ...      ...
95 2024-02-01 04:03:25.351272711  185.97     2        Q
96 2024-02-01 04:03:25.351544878  185.90   100        Q
97 2024-02-01 04:03:25.351546823  185.88   648        Q
98 2024-02-01 04:03:25.351553003  185.88   117        Q
99 2024-02-01 04:03:25.351703930  185.87   128        P
...
```

##### SEE ALSO
**BYTE_PRESENT** OneTick event processor

``character_present()``

