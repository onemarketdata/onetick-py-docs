# otp.ops.sametime

### ``sametime(left_time, right_time, keep_zero_duration_ticks=None)``

Returns **True** for a tick from the left source and the tick from the right source
which arrived immediately before it, and vice versa
(for a tick from the right source and the tick from the left source which arrived immediately before it).

Can be used only in the `on` parameter of ``onetick.py.join()``.

* **Parameters:**
  * **left_time** (``Column``) – Timestamp column of the left source (`left['TIMESTAMP']`).
  * **right_time** (``Column``) – Timestamp column of the right source (`right['TIMESTAMP']`).
  * **keep_zero_duration_ticks** (*bool*) – 

    If **False**, output ticks that last zero time are discarded from the output.

    Such ticks can result when some ticks in the first time series have the same timestamps
    as the ticks in the other time series. When a tick from the first time series arrives,
    the corresponding tick with the same timestamp from the other time series might not have arrived yet,
    so that the output tick would contain the new tick from the first time series and the oldest tick
    from the second time series. However, when a new tick from the second time series (with the same timestamp)
    arrives, the computed output tick contains new ticks from the first and second time series.
    Timestamps of the output ticks would be the same, and the first output tick would be undesirable;
    for example when joining two same-sized vectors.

    Default is **True**.
* **Return type:**
  ``Operation``

##### Examples

Join each tick with the tick from the other source that arrived immediately before it:

```
>>> left = otp.Ticks(A=[1, 2, 3], offset=[0, 2, 4])
>>> right = otp.Ticks(B=[10, 20, 30], offset=[1, 3, 5])
>>> data = otp.join(left, right, on=otp.ops.sametime(left['TIMESTAMP'], right['TIMESTAMP']), how='inner')
>>> otp.run(data)
                     Time  A   B
0 2003-12-01 00:00:00.001  1  10
1 2003-12-01 00:00:00.002  2  10
2 2003-12-01 00:00:00.003  2  20
3 2003-12-01 00:00:00.004  3  20
4 2003-12-01 00:00:00.005  3  30
```

Zero-duration ticks can be discarded with `keep_zero_duration_ticks=False`:

```
>>> left = otp.Ticks(A=[1, 2, 3])
>>> right = otp.Ticks(B=[10, 20, 30])
>>> data = otp.join(left, right, on=otp.ops.sametime(left['TIMESTAMP'], right['TIMESTAMP']), how='inner')
>>> otp.run(data)
                     Time  A   B
0 2003-12-01 00:00:00.000  1  10
1 2003-12-01 00:00:00.001  2  10
2 2003-12-01 00:00:00.001  2  20
3 2003-12-01 00:00:00.002  3  20
4 2003-12-01 00:00:00.002  3  30
```

```
>>> data = otp.join(left, right,
...                 on=otp.ops.sametime(left['TIMESTAMP'], right['TIMESTAMP'], keep_zero_duration_ticks=False),
...                 how='inner')
>>> otp.run(data)
                     Time  A   B
0 2003-12-01 00:00:00.000  1  10
1 2003-12-01 00:00:00.001  2  20
2 2003-12-01 00:00:00.002  3  30
```

##### SEE ALSO
``onetick.py.join()``

``onetick.py.ops.sametime_as_existing()``

**SAMETIME** OneTick function

**JOIN** OneTick event processor

