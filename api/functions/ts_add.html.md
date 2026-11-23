# otp.ts_add

### ``ts_add(sources, input_field_name=None, , , bucket_interval=0, bucket_units=None, bucket_time='end', bucket_end_condition=None, boundary_tick_bucket='new', running=False, symbols=None)``

Computes the sum of fields’ latest values across multiple series.

Outputs a time series of ticks with the summed field **VALUE**
and the field named **NUM_SYMBOLS** containing the number of values that went into computing the sum.

* **Parameters:**
  * **sources** (``Source`` or list of ``Source``) – One or more aggregated sources.
  * **input_field_name** (*str*) – The name of the input field to sum.
    Default is ‘PRICE’.
  * **symbols** (str, list of str, ``Source``, `pandas.DataFrame`) – Symbol name or list of symbol names or the first-stage query
    representing the symbols used to sum the value across.
  * **bucket_interval** (int or float or ``Operation`` or ``OnetickParameter`` or ``symbol parameter`` or `datetime offset object`, default=0) – 

    Determines the length of each bucket (units depends on `bucket_units`).

    If ``Operation`` of bool type is passed, acts as `bucket_end_condition`.

    Bucket interval can also be set as a *float* value
    if `bucket_units` is set to *seconds*.
    Note that values less than 0.001 (1 millisecond) are not supported.

    Bucket interval can be set via some of the `datetime offset objects`:
    ``otp.Milli``, ``otp.Second``,
    ``otp.Minute``, ``otp.Hour``,
    ``otp.Day``, ``otp.Month``.
    In this case you could omit setting `bucket_units` parameter.

    Bucket interval can also be set with integer ``OnetickParameter``
    or ``symbol parameter``.
  * **bucket_units** (*Optional* *[**Literal* *[* *'seconds'* *,*  *'ticks'* *,*  *'days'* *,*  *'months'* *,*  *'flexible'* *]* *]* *,* *default=None*) – 

    Set bucket interval units.

    By default, if `bucket_units` and `bucket_end_condition` not specified, set to **seconds**.
    If `bucket_end_condition` specified, then `bucket_units` set to **flexible**.

    If set to **flexible** then `bucket_end_condition` must be set.

    Note that **seconds** bucket unit doesn’t take into account daylight-saving time of the timezone,
    so you may not get expected results when using, for example, 24 \* 60 \* 60 seconds as bucket interval.
    In such case use **days** bucket unit instead.
    See example in ``onetick.py.agg.sum()``.
  * **bucket_time** (*Literal* *[* *'start'* *,*  *'end'* *]* *,* *default=end*) – 

    Control output timestamp.
    * **start**

      the timestamp  assigned to the bucket is the start time of the bucket.
    * **end**

      the timestamp assigned to the bucket is the end time of the bucket.
  * **bucket_end_condition** (*condition* *,* *default=None*) – 

    An expression that is evaluated on every tick. If it evaluates to “True”, then a new bucket is created.
    This parameter is only used if `bucket_units` is set to “flexible”.

    Also can be set via `bucket_interval` parameter by passing ``Operation`` object.
  * **boundary_tick_bucket** (*Literal* *[* *'new'* *,*  *'previous'* *]* *,* *default=new*) – 

    Controls boundary tick ownership.
    * **previous**

      A tick on which `bucket_end_condition` evaluates to “true” belongs to the bucket being closed.
    * **new**

      tick belongs to the new bucket.

    This parameter is only used if `bucket_units` is set to “flexible”
  * **running** (*bool* *,* *default=False*) – 

    See `Aggregation buckets guide` to see examples of how this parameter works.

    Specifies if the aggregation will be calculated as a sliding window.
    `running` and `bucket_interval` parameters determines when new buckets are created.
    * `running` = True

      aggregation will be calculated in a sliding window.
      * `bucket_interval` = N (N > 0)

        Window size will be N. Output tick will be generated when tick “enter” window (**arrival event**) and
        when “exit” window (**exit event**)
      * `bucket_interval` = 0

        Left boundary of window will be set to query start time. For each tick aggregation will be calculated in
        the interval [start_time; tick_t] from query start time to the tick’s timestamp (inclusive).
    * `running` = False (default)

      buckets partition the [query start time, query end time) interval into non-overlapping intervals
      of size `bucket_interval` (with the last interval possibly of a smaller size).
      If `bucket_interval` is set to **0** a single bucket for the entire interval is created.

      Note that in non-running mode OneTick unconditionally divides the whole time interval
      into specified number of buckets.
      It means that you will always get this specified number of ticks in the result,
      even if you have less ticks in the input data.

    Default: False

##### Examples

Get the sum of latest hourly SIZE values from two sources:

```
>>> aapl = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> msft = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='MSFT')
>>> data = otp.ts_add([aapl, msft], 'SIZE', bucket_interval=otp.Hour(1))
>>> otp.run(data, start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time  VALUE  NUM_SYMBOLS
0 2024-02-01 10:30:00  124.0            2
1 2024-02-01 11:30:00    6.0            2
2 2024-02-01 12:30:00   52.0            2
3 2024-02-01 13:30:00   51.0            2
4 2024-02-01 14:30:00   31.0            2
5 2024-02-01 15:30:00    6.0            2
6 2024-02-01 16:00:00   14.0            2
```

Get the sum of latest hourly SIZE values from three symbols:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
>>> data = otp.ts_add(data, 'SIZE', bucket_interval=otp.Hour(1), symbols=['AAPL', 'MSFT', 'NVDA'])
>>> otp.run(data, start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time  VALUE  NUM_SYMBOLS
0 2024-02-01 10:30:00  125.0            3
1 2024-02-01 11:30:00   13.0            3
2 2024-02-01 12:30:00   53.0            3
3 2024-02-01 13:30:00   61.0            3
4 2024-02-01 14:30:00   32.0            3
5 2024-02-01 15:30:00    8.0            3
6 2024-02-01 16:00:00   78.0            3
```

Use this together with other aggregations to aggregate across symbols.
For example, hourly total traded volume (sum of SIZE) across symbols starting with A:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
>>> data = data.agg({'VOLUME': otp.agg.sum('SIZE')}, bucket_interval=otp.Hour(1))
>>> symbols = otp.Symbols('US_COMP_SAMPLE', for_tick_type='TRD', pattern='A%')
>>> data = otp.ts_add(data, 'VOLUME', bucket_interval=otp.Hour(1), symbols=symbols)
>>> otp.run(data, start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time       VALUE  NUM_SYMBOLS
0 2024-02-01 10:30:00  74155047.0           50
1 2024-02-01 11:30:00  43958426.0           50
2 2024-02-01 12:30:00  36254186.0           50
3 2024-02-01 13:30:00  39337805.0           50
4 2024-02-01 14:30:00  38059030.0           50
5 2024-02-01 15:30:00  41425091.0           50
6 2024-02-01 16:00:00  46796480.0           50
```

##### SEE ALSO
**TS_ADD** OneTick event processor
