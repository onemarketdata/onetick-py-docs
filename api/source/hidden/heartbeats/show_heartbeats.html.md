# otp.Source.show_heartbeats

#### ``Source.show_heartbeats(listen_mode='active', inplace=False)``

Generates a tick per heartbeat (timer event).

Output ticks have only one field *CURRENT_TIME* which carries the time of the heartbeat.

* **Parameters:**
  * **listen_mode** (*str*) – 

    Heartbeat listening mode, possible values are `active` (default) and `passive`.

    If the listening mode is `active`, then all possible heartbeats which can be passed to the query
    are shown.
    Otherwise heartbeats are shown with the same frequency as they would be passed to the query
    without this method.

    For example, if a query consists of a single aggregation with time buckets,
    then it will get a heartbeat once per each bucket interval.
    But after adding this method with `active` listening mode the frequency of heartbeats will increase
    to the maximal possible value and they will be shown.
    To see the heartbeats of the same frequency as in the initial query, `passive` listening mode
    should be used.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Insert a heartbeat before each tick with *SIZE* bigger than 100 and show inserted heartbeats:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']]
>>> data = data.insert_heartbeat(where=data['SIZE'] > 100)
>>> data = data.show_heartbeats()
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                            Time                  CURRENT_TIME
0  2024-02-01 04:00:00.008291153 2024-02-01 04:00:00.008291153
1  2024-02-01 04:00:00.124644495 2024-02-01 04:00:00.124644495
2  2024-02-01 04:00:17.426836387 2024-02-01 04:00:17.426836387
3  2024-02-01 04:00:25.083671012 2024-02-01 04:00:25.083671012
4  2024-02-01 04:03:25.351156225 2024-02-01 04:03:25.351156225
...
```

##### SEE ALSO
**SHOW_HEARTBEATS** OneTick event processor

``insert_heartbeat()``

``intercept_heartbeats()``

