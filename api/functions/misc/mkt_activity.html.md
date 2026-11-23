# otp.ops.mkt_activity

### ``mkt_activity(calendar_name)``

Returns a string with a value
similar to ``onetick.py.Source.mkt_activity()`` **MKT_ACTIVITY** field
for the specified `calendar_name`.

* **Parameters:**
  **calendar_name** (str or ``Operation``) – The calendar name to choose for the respective calendar from the *CALENDAR* sections of the reference database.
  It can be a string constant or the name of the field with per-tick calendar name.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']].limit(5)
>>> data['MKT_ACTIVITY'] = otp.ops.mkt_activity('CLOUD_DB_US_COMP')
>>> otp.run(data, date=otp.date(2024, 2, 1))
                           Time   PRICE  SIZE MKT_ACTIVITY
0 2024-02-01 04:00:00.008283417  186.50     6           Rb
1 2024-02-01 04:00:00.008290927  185.59     1           Rb
2 2024-02-01 04:00:00.008291153  185.49   107           Rb
3 2024-02-01 04:00:00.010381671  185.49     1           Rb
4 2024-02-01 04:00:00.011224206  185.50     2           Rb
```

##### SEE ALSO
**MKT_ACTIVITY** OneTick function

``onetick.py.Source.mkt_activity()``

