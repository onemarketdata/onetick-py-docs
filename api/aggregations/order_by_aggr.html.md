# otp.agg.order_by_aggr

### ``order_by_aggr(bucket_interval=0, bucket_units=None, running=False, bucket_time='end', bucket_end_condition=None, boundary_tick_bucket='new', group_by=None, groups_to_display='all', end_condition_per_group=False, keep_timestamp=True, *args, order_by, num_ticks, **kwargs)``

For each bucket propagates at most `num_ticks` sorted ticks,
where sorting is done using the specified set of `order_by` fields.

* **Parameters:**
  * **order_by** (*str* *or* *list* *or* *dict*) – Set of fields to sort by.
    Can be one field specified by string, list of fields or dictionary with field names
    as keys and `asc` or `desc` string literals as values. Latter allows to specify
    sorting direction. Default direction is `desc`.
  * **num_ticks** (*int*) – The number of sorted ticks to be propagated for each bucket.
    Special value `ALL` will propagate every tick in each bucket.
    Default: 1.
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
  * **group_by** (*list* *,* *str* *or* *expression* *,* *default=None*) – When specified, each bucket is broken further into additional sub-buckets based on specified field values.
    If ``Operation`` is used then GROUP_{i} column is added. Where i is index in group_by list.
    For example, if Operation is the only element in `group_by` list then GROUP_0 field will be added.
  * **groups_to_display** (*Literal* *[* *'all'* *,*  *'previous'* *]* *,* *default=all*) – Specifies for which sub-buckets (groups) ticks should be shown for each bucket interval.
    By default **all** groups are shown at the end of each bucket interval.
    If this parameter is set to **event_in_last_bucket**, only the groups that received at least one tick
    within a given bucket interval are shown.
  * **end_condition_per_group** (*bool* *,* *default=False*) – 

    Controls application of `bucket_end_condition` in groups.
    * `end_condition_per_group` = True

      `bucket_end_condition` is applied only to the group defined by `group_by`
    * `end_condition_per_group` = False

      `bucket_end_condition` applied across all groups

    This parameter is only used if `bucket_units` is set to “flexible”.

    When set to True, applies to all bucketing conditions. Useful, for example, if you need to specify `group_by`,
    and you want to group items first, and create buckets after that.
  * **keep_timestamp** (*bool* *,* *default=True*) – If True, timestamps of the output ticks are the same as timestamps of the original ticks.
    Otherwise, timestamps of the output ticks are determined by bucket_time, and original timestamps
    are put in the TICK_TIME field.

##### Examples

Get the biggest price every hour:

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']]
>>> data = data.order_by_aggr('PRICE', bucket_interval=otp.Hour(1))
>>> otp.run(data, start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                           Time     PRICE  SIZE
0 2024-02-01 10:29:46.337467789  186.1800   100
1 2024-02-01 10:53:56.130163522  192.4200     6
2 2024-02-01 12:21:16.907282289  188.6050   375
3 2024-02-01 12:58:30.442440693  192.6000   200
4 2024-02-01 14:26:03.462445251  186.1667    96
5 2024-02-01 14:44:08.734358075  190.9400    48
6 2024-02-01 15:59:44.208724181  186.9500     1
```

Get two biggest prices every hour and also sort by size
(note that parameter `keep_timestamp=False` should be set to keep the sorting,
otherwise original timestamps will be kept and the sorting will be done by them):

```
>>> data = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']]
>>> data = data.order_by_aggr(
...     {'PRICE': 'desc', 'SIZE': 'desc'},
...     num_ticks=2,
...     bucket_interval=otp.Hour(1),
...     keep_timestamp=False,
... )
>>> otp.run(data, start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                  Time     PRICE   SIZE                     TICK_TIME
0  2024-02-01 10:30:00  186.1800    150 2024-02-01 10:29:46.337479730
1  2024-02-01 10:30:00  186.1800    100 2024-02-01 10:29:46.337467789
2  2024-02-01 11:30:00  192.4200      6 2024-02-01 10:53:56.130163522
3  2024-02-01 11:30:00  186.3100    200 2024-02-01 10:47:44.894150035
4  2024-02-01 12:30:00  188.6050    375 2024-02-01 12:21:16.907282289
5  2024-02-01 12:30:00  186.3000     43 2024-02-01 12:09:07.300341874
6  2024-02-01 13:30:00  192.6000    200 2024-02-01 12:58:30.442440693
7  2024-02-01 13:30:00  186.4400   1000 2024-02-01 12:55:48.679609428
8  2024-02-01 14:30:00  186.1667     96 2024-02-01 14:26:03.462445251
9  2024-02-01 14:30:00  186.1666     48 2024-02-01 14:26:03.462235331
10 2024-02-01 15:30:00  190.9400     48 2024-02-01 14:44:08.734358075
11 2024-02-01 15:30:00  186.8000    100 2024-02-01 15:26:16.993395799
12 2024-02-01 16:00:00  186.9500  10564 2024-02-01 15:59:44.208768253
13 2024-02-01 16:00:00  186.9500   2600 2024-02-01 15:59:44.208757524
```

##### SEE ALSO
**ORDER_BY_AGGR** OneTick event processor
