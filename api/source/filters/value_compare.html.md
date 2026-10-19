# otp.Source.value_compare

#### ``Source.value_compare(field, relationship_to_const, value, , , discard_on_match=False, inplace=False)``

Propagates ticks based on whether the value in the `field`
is in the specified `relationship_to_const` to the `value`.

* **Parameters:**
  * **field** (str, ``Column``) – The name of the field to apply filter to.
  * **relationship_to_const** (*str*) – 

    Relationship to check between the value of the `field` and constant `value`.
    Supported values:
    * `lt` (less),
    * `le` (less or equal),
    * `eq` (equal),
    * `ne` (not equal),
    * `ge` (greater or equal),
    * `gt` (greater).
  * **value** (*str* *,* *int*) – The value to compare the `field` to.
    Only string and numeric values are supported.
  * **discard_on_match** (*bool*) – If this parameter is False (default), only ticks that match the filter will be propagated.
    Otherwise ticks that match the filter will be discarded.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Propagate only the ticks where field EXCHANGE equals to P character:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE', 'EXCHANGE']]
>>> data = data.value_compare('EXCHANGE', 'eq',  'P')
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1), timezone='America/New_York')
                            Time   PRICE  SIZE EXCHANGE
0  2024-02-01 04:00:00.033759205  185.90    16        P
1  2024-02-01 04:00:00.169091123  185.90    87        P
2  2024-02-01 04:00:00.413581861  185.98     1        P
3  2024-02-01 04:00:00.721593975  185.77     6        P
4  2024-02-01 04:00:00.721594183  185.76     1        P
..                           ...     ...   ...      ...
95 2024-02-01 04:07:38.594705586  185.81    10        P
96 2024-02-01 04:07:47.740645808  185.81     7        P
97 2024-02-01 04:07:47.740649834  185.81     1        P
98 2024-02-01 04:07:58.714205622  185.86     5        P
99 2024-02-01 04:07:59.902144628  185.81     7        P
...
```

##### SEE ALSO
**VALUE_COMPARE** OneTick event processor
