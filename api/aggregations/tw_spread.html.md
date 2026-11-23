# otp.agg.tw_spread

### ``tw_spread(running=False, all_fields=False, bucket_interval=0, bucket_time='end', bucket_units=None, bucket_end_condition=None, end_condition_per_group=False, boundary_tick_bucket='new', group_by=None, groups_to_display='all', output_field_name=None, *args, in_basis_points, positive_spread_only, **kwargs)``

For each bucket, computes the time-weighted spread between the `BID_PRICE` and the `ASK_PRICE`.

* **Parameters:**
  * **in_basis_points** (*bool*) – Determines if the spread is to be converted to basis points (percentage of mid-quote) – default,
    or absolute monetary units.
  * **positive_spread_only** (*bool*) – When set to True (default), only ticks with positive spread will be used in the computation.
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
  * **all_fields** (*Union* **[*bool* *,* *str* *]* *,* *default=False*) – 

    See `Aggregation buckets guide` to see examples of how this parameter works.
    * `all_fields` = True

      output ticks include all fields from the input ticks
      * `running` = True

      an output tick is created only when a tick enters the sliding window
      * `running` = False

      fields of first tick in bucket will be used
    * `all_fields` = False and `running` = True

      output ticks are created when a tick enters or leaves the sliding window.
    * `all_fields` = “when_ticks_exit_window” and `running` = True

      output ticks are generated only for exit events, but all attributes from the exiting tick are copied over
      to the output tick and the aggregation is added as another attribute.
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
  * **bucket_time** (*Literal* *[* *'start'* *,*  *'end'* *]* *,* *default=end*) – 

    Control output timestamp.
    * **start**

      the timestamp  assigned to the bucket is the start time of the bucket.
    * **end**

      the timestamp assigned to the bucket is the end time of the bucket.
  * **bucket_units** (*Optional* *[**Literal* *[* *'seconds'* *,*  *'ticks'* *,*  *'days'* *,*  *'months'* *,*  *'flexible'* *]* *]* *,* *default=None*) – 

    Set bucket interval units.

    By default, if `bucket_units` and `bucket_end_condition` not specified, set to **seconds**.
    If `bucket_end_condition` specified, then `bucket_units` set to **flexible**.

    If set to **flexible** then `bucket_end_condition` must be set.

    Note that **seconds** bucket unit doesn’t take into account daylight-saving time of the timezone,
    so you may not get expected results when using, for example, 24 \* 60 \* 60 seconds as bucket interval.
    In such case use **days** bucket unit instead.
    See example in ``onetick.py.agg.sum()``.
  * **bucket_end_condition** (*condition* *,* *default=None*) – 

    An expression that is evaluated on every tick. If it evaluates to “True”, then a new bucket is created.
    This parameter is only used if `bucket_units` is set to “flexible”.

    Also can be set via `bucket_interval` parameter by passing ``Operation`` object.
  * **end_condition_per_group** (*bool* *,* *default=False*) – 

    Controls application of `bucket_end_condition` in groups.
    * `end_condition_per_group` = True

      `bucket_end_condition` is applied only to the group defined by `group_by`
    * `end_condition_per_group` = False

      `bucket_end_condition` applied across all groups

    This parameter is only used if `bucket_units` is set to “flexible”.

    When set to True, applies to all bucketing conditions. Useful, for example, if you need to specify `group_by`,
    and you want to group items first, and create buckets after that.
  * **boundary_tick_bucket** (*Literal* *[* *'new'* *,*  *'previous'* *]* *,* *default=new*) – 

    Controls boundary tick ownership.
    * **previous**

      A tick on which `bucket_end_condition` evaluates to “true” belongs to the bucket being closed.
    * **new**

      tick belongs to the new bucket.

    This parameter is only used if `bucket_units` is set to “flexible”
  * **group_by** (*list* *,* *str* *or* *expression* *,* *default=None*) – When specified, each bucket is broken further into additional sub-buckets based on specified field values.
    If ``Operation`` is used then GROUP_{i} column is added. Where i is index in group_by list.
    For example, if Operation is the only element in `group_by` list then GROUP_0 field will be added.
  * **groups_to_display** (*Literal* *[* *'all'* *,*  *'previous'* *]* *,* *default=all*) – Specifies for which sub-buckets (groups) ticks should be shown for each bucket interval.
    By default **all** groups are shown at the end of each bucket interval.
    If this parameter is set to **event_in_last_bucket**, only the groups that received at least one tick
    within a given bucket interval are shown.
  * **output_field_name** (*str* *|* *None* *,* *default=None*) – 

    Output field name of the aggregation.

    If not set, then, depending on the type of aggregation,
    either the input field name will be used (if there is only one input of the aggregation),
    or the new column with some predefined name will be created
    (usually `VALUE` or uppercased name of the aggregation).

##### Examples

Using aggregation as a ``otp.Source.tw_spread`` method:

By default only the positive spreads are used and the result is calculated in basis points:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> data = data.tw_spread(output_field_name='TW_SPREAD', bucket_interval=otp.Hour(1))
>>> otp.run(data, start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time  TW_SPREAD
0 2024-02-01 10:30:00  60.110560
1 2024-02-01 11:30:00  27.862491
2 2024-02-01 12:30:00  19.548332
3 2024-02-01 13:30:00  26.548615
4 2024-02-01 14:30:00  26.854572
5 2024-02-01 15:30:00  24.714366
6 2024-02-01 16:00:00  12.483197
```

Using in ``agg()`` method with other aggregations.

Using all spreads and calculating results in absolute monetary units, basically
getting the same result as with ``tw_average()``

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE', symbols='AAPL')
>>> data['SPREAD'] = data['ASK_PRICE'] - data['BID_PRICE']
>>> data = data.agg({
...     'TW_SPREAD': otp.agg.tw_spread(in_basis_points=False, positive_spread_only=False),
...     'TW_AVERAGE': otp.agg.tw_average('SPREAD'),
... }, bucket_interval=otp.Hour(1))
>>> otp.run(data, start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time  TW_SPREAD  TW_AVERAGE
0 2024-02-01 10:30:00   1.095853    1.095853
1 2024-02-01 11:30:00   0.520080    0.520080
2 2024-02-01 12:30:00   0.365623    0.365623
3 2024-02-01 13:30:00   0.497084    0.497084
4 2024-02-01 14:30:00   0.502917    0.502917
5 2024-02-01 15:30:00   0.464956    0.464956
6 2024-02-01 16:00:00   0.127003    0.127003
```

##### SEE ALSO
**TW_SPREAD** OneTick event processor

``tw_average()``

