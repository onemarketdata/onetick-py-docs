# otp.timedelta

### ``class timedelta(value=<object object>, unit=None, **kwargs)``

Bases: `Timedelta`

The object representing the delta between timestamps.

* **Parameters:**
  * **value** (``otp.timedelta``, `pandas.Timedelta`,           ``datetime.timedelta``, str, or int) – Initialize this object from other types of objects.
  * **kwargs** – Dictionary of offset names and their values.
    Available offset names:
    *weeks*, *days*, *hours*, *minutes*, *seconds*,
    *milliseconds*, *microseconds*, *nanoseconds*.

##### Examples

Create ``otp.timedelta`` from key-value arguments:

```
>>> otp.timedelta(weeks=1, days=1, hours=1, minutes=1, seconds=1, milliseconds=1, microseconds=1, nanoseconds=1)
timedelta('8 days 01:01:01.001001001')
```

Create ``otp.timedelta`` from different types of objects:

```
>>> otp.timedelta(datetime.timedelta(days=2, hours=3))
timedelta('2 days 03:00:00')
```

```
>>> otp.timedelta('20 days 13:02:01.999777666')
timedelta('20 days 13:02:01.999777666')
```

Adding ``otp.timedelta`` object to ``otp.datetime``:

```
>>> otp.datetime(2022, 1, 1, 1, 2, 3) + otp.timedelta(days=1, hours=1, minutes=1, seconds=1)
2022-01-02 02:03:04
```

Adding ``otp.timedelta`` object to ``otp.date``:

```
>>> otp.date(2022, 1, 1) + otp.timedelta(weeks=1, nanoseconds=1)
2022-01-08 00:00:00.000000001
```

Adding ``otp.timedelta`` object to ``otp.Operation``:

```
>>> t = otp.Tick(A=1)
>>> t['X'] = t['_START_TIME'] + otp.timedelta(hours=5)
>>> otp.run(t, date=otp.dt(2022, 1, 1))
        Time  A                   X
0 2022-01-01  1 2022-01-01 05:00:00
```
