# otp.matches_time_filter

### ``matches_time_filter(start_time, end_time, timezone=None, day_patterns=None, end_time_tick_matches=None)``

Returns True if a tick matches the specified time filter criteria,
including a time range and optional day patterns.

* **Parameters:**
  * **start_time** (int | str | ``Operation``) – 

    The start and end times of the filter, specified as either an integer or a string.

    Accepted formats:
    * *HHMMSS*: For example, 093000 for 9:30 AM
    * *HHMMSSmmm*: For example, 093000000 for 9:30:00.000 AM.
    * *HH:MM:SS[.mmm]*: For example, “09:30:00.000” for 9:30 AM.
  * **end_time** (int | str | ``Operation``) – 

    The start and end times of the filter, specified as either an integer or a string.

    Accepted formats:
    * *HHMMSS*: For example, 093000 for 9:30 AM
    * *HHMMSSmmm*: For example, 093000000 for 9:30:00.000 AM.
    * *HH:MM:SS[.mmm]*: For example, “09:30:00.000” for 9:30 AM.
  * **timezone** (str | ``Operation``) – 

    The timezone to use.

    By default the timezone of the query is used.
  * **day_patterns** (str or ``Operation``) – A string representing day patterns that define when ticks should be propagated.
    For more details and examples of supported formats, refer to the ``onetick.py.Source.time_filter()``.
  * **end_time_tick_matches** (bool or ``Operation``) – 

    A flag indicating whether ticks at the `end_time` boundary
    should be considered within the filter range.

    Defaults to False.
* **Return type:**
  ``Operation``

##### Examples

Set flag for each timestamp from 02:30 till 06:00:

```
>>> data = otp.Ticks(A=range(8), offset=[otp.Hour(i) for i in range(8)])
>>> data['X'] = otp.matches_time_filter('023000', '060000')
>>> otp.run(data)
                 Time  A    X
0 2003-12-01 00:00:00  0  0.0
1 2003-12-01 01:00:00  1  0.0
2 2003-12-01 02:00:00  2  0.0
3 2003-12-01 03:00:00  3  1.0
4 2003-12-01 04:00:00  4  1.0
5 2003-12-01 05:00:00  5  1.0
6 2003-12-01 06:00:00  6  0.0
7 2003-12-01 07:00:00  7  0.0
```

Set parameter `end_time_tick_matches` to include `end_time` in the range:

```
>>> data = otp.Ticks(A=range(8), offset=[otp.Hour(i) for i in range(8)])
>>> data['X'] = otp.matches_time_filter('023000', '060000', end_time_tick_matches=True)
>>> otp.run(data)
                 Time  A    X
0 2003-12-01 00:00:00  0  0.0
1 2003-12-01 01:00:00  1  0.0
2 2003-12-01 02:00:00  2  0.0
3 2003-12-01 03:00:00  3  1.0
4 2003-12-01 04:00:00  4  1.0
5 2003-12-01 05:00:00  5  1.0
6 2003-12-01 06:00:00  6  1.0
7 2003-12-01 07:00:00  7  0.0
```

##### SEE ALSO
``onetick.py.Source.time_filter()``

**MATCHES_TIME_FILTER** OneTick function

**TIME_FILTER** OneTick event processor

