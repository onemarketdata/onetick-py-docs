# otp.ops.sametime_as_existing

### ``sametime_as_existing(left_time, right_time, delay_msec)``

If `delay_msec` is positive, it returns **True** for a tick from the passed left time series and the latest tick
from the passed right time series that arrived at least by `delay_msec` before the tick from the left time series.

If `delay_msec` is negative, it returns **True** for a tick from the passed left time series and the latest tick
from the passed right time series that arrived at most `delay_msec` after the tick from the left time series;
that is, the latest tick from the interval `(-Inf, t1 + |delay_msec|]`, where `t1` is the timestamp of the tick
from the left time series.

Can be used only in the `on` parameter of ``onetick.py.join()``.

* **Parameters:**
  * **left_time** (``Column``) – Timestamp column of the left source (`left['TIMESTAMP']`).
  * **right_time** (``Column``) – Timestamp column of the right source (`right['TIMESTAMP']`).
  * **delay_msec** (*int*) – Delay in milliseconds.
* **Return type:**
  ``Operation``

##### Examples

Join each tick from the left source with the latest tick from the right source
that arrived at least 2 milliseconds before it:

```
>>> left = otp.Ticks(A=[1, 2, 3], offset=[3, 5, 7])
>>> right = otp.Ticks(B=[10, 20, 30, 40], offset=[0, 2, 4, 6])
>>> data = otp.join(left, right, on=otp.ops.sametime_as_existing(left['TIMESTAMP'], right['TIMESTAMP'], 2))
>>> otp.run(data)
                     Time  A   B
0 2003-12-01 00:00:00.003  1  10
1 2003-12-01 00:00:00.005  2  20
2 2003-12-01 00:00:00.007  3  30
```

With negative delay ticks from the right source that arrived less than 2 milliseconds after
the tick from the left source are also considered:

```
>>> data = otp.join(left, right, on=otp.ops.sametime_as_existing(left['TIMESTAMP'], right['TIMESTAMP'], -2))
>>> otp.run(data)
                     Time  A   B
0 2003-12-01 00:00:00.003  1  30
1 2003-12-01 00:00:00.005  2  40
2 2003-12-01 00:00:00.007  3  40
```

##### SEE ALSO
``onetick.py.join()``

``onetick.py.ops.sametime()``

**SAMETIME_AS_EXISTING** OneTick function

**JOIN** OneTick event processor

