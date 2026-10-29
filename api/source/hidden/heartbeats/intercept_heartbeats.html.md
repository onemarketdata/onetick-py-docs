# otp.Source.intercept_heartbeats

#### ``Source.intercept_heartbeats(inplace=False)``

Intercepts heartbeats (timer events), leaving all other events of the time series unchanged.

* **Parameters:**
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Assume we have heartbeats and data quality events in the data flow:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']]
>>> data = data.insert_heartbeat(where=data['SIZE'] > 1000)
>>> data = data.insert_data_quality_event('OK', where=data['SIZE'] > 5000)
```

Intercepting heartbeats removes only heartbeats, data quality events are left unchanged:

```
>>> data = data.intercept_heartbeats()
>>> otp.run(data.show_heartbeats(), date=otp.dt(2024, 2, 1))
Empty DataFrame
...
```

```
>>> otp.run(data.show_data_quality(), date=otp.dt(2024, 2, 1))
                             Time  DATA_QUALITY_TYPE DATA_QUALITY_NAME
0   2024-02-01 08:00:00.074574483                  0                OK
1   2024-02-01 08:00:00.074937867                  0                OK
2   2024-02-01 08:00:00.075738202                  0                OK
3   2024-02-01 09:00:06.565175834                  0                OK
4   2024-02-01 09:24:20.329799843                  0                OK
...
```

##### SEE ALSO
**INTERCEPT_HEARTBEATS** OneTick event processor

``insert_heartbeat()``

``show_heartbeats()``

