# otp.Source.insert_heartbeat

#### ``Source.insert_heartbeat(where=None, insert_before=True, inplace=False)``

Injects timer events (heartbeats) into the data flow.

Heartbeats are not visible in the output of the query,
use ``show_heartbeats()`` to see them.

* **Parameters:**
  * **where** (str or ``Operation``) – Specifies a criterion for the selection of ticks whose arrival results in generation of a heartbeat.
    If this expression returns True, a heartbeat will be inserted into a time series.
    The expression can also be empty (default), in which case each input tick generates a heartbeat.
  * **insert_before** (*bool*) – If True (default), generated heartbeat will be inserted before the input tick that triggered its creation,
    otherwise generated heartbeat will be inserted after that input tick.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Insert a heartbeat before each tick with *SIZE* bigger than 100.
Heartbeats are not visible, so the output is not changed:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']]
>>> data = data.insert_heartbeat(where=data['SIZE'] > 100)
>>> data = data.limit(5)
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                           Time   PRICE  SIZE
0 2024-02-01 04:00:00.008283417  186.50     6
1 2024-02-01 04:00:00.008290927  185.59     1
2 2024-02-01 04:00:00.008291153  185.49   107
3 2024-02-01 04:00:00.010381671  185.49     1
4 2024-02-01 04:00:00.011224206  185.50     2
```

Now use ``show_heartbeats()`` to see inserted heartbeats:

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
**INSERT_HEARTBEAT** OneTick event processor

``show_heartbeats()``

``intercept_heartbeats()``

