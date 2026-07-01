# otp.Source.show_hidden_ticks

#### ``Source.show_hidden_ticks(inplace=False)``

Propagates all of a tick’s fields without changing their values. Propagates all ticks,
even those with a status not equal to 0, which are normally hidden.

Use this method to display all original ticks and correction ticks in the same time series in the same
time sequence in which they were originally sent with a filter to remove unneeded **TICK_STATUS** values.

* **Parameters:**
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Show hidden ticks and filter them by choosing non-zero *TICK_STATUS* values:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data.show_hidden_ticks()
>>> data = data.where(data['TICK_STATUS'] != 0)
>>> data = data[['PRICE', 'SIZE', 'TICK_STATUS']]
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                            Time     PRICE  SIZE  TICK_STATUS
0  2024-02-01 11:50:15.621123654  185.6950     1            1
