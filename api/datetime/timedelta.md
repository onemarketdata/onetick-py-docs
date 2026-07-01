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
