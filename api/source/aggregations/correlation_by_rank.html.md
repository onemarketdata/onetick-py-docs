# otp.Source.correlation_by_rank

#### ``Source.correlation_by_rank(bucket_interval=0, bucket_units=None, running=False, bucket_time='end', bucket_end_condition=None, boundary_tick_bucket='new', group_by=None, groups_to_display='all', end_condition_per_group=False, output_field_name=None, *args, column_name_1, column_name_2, input_is_ranks, **kwargs)``

Computes the Spearman rank correlation value between two numeric fields in the aggregation bucket.

* **Parameters:**
  * **column_name_1** (*str*) – The name of the field in the input stream whose value is to be used by the aggregation
  * **column_name_2** (*str*) – The name of the field in the input stream whose value is to be used by the aggregation
  * **input_is_ranks** (*bool*) – Can be set if input fields contains ranks (see ``ranking()``).
    Default is False.
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
  * **output_field_name** (*str* *|* *None* *,* *default=None*) – 

    Output field name of the aggregation.

    If not set, then, depending on the type of aggregation,
    either the input field name will be used (if there is only one input of the aggregation),
    or the new column with some predefined name will be created
    (usually `VALUE` or uppercased name of the aggregation).
* **Return type:**
  `Source`

##### Examples

Using aggregation as a ``otp.Source.correlation_by_rank`` method:

```
>>> data = otp.Ticks(X=[106, 100, 86, 101, 99, 103, 97, 113, 112, 110],
...                  Y=[7, 27, 2, 50, 28, 29, 20, 12, 6, 17])
>>> data = data.correlation_by_rank('X', 'Y')
>>> otp.run(data)
        Time  CORRELATION_BY_RANK
0 2003-12-04            -0.175758
```

Using in ``agg()`` method with other aggregations:

```
>>> data = otp.Ticks(X=[106, 100, 86, 101, 99, 103, 97, 113, 112, 110],
...                  Y=[7, 27, 2, 50, 28, 29, 20, 12, 6, 17])
>>> data = data.agg({
...     'CBR': otp.agg.correlation_by_rank('X', 'Y'),
...     'SUM_X': otp.agg.sum('X'),
... })
>>> otp.run(data)
        Time       CBR  SUM_X
0 2003-12-04 -0.175758   1027
```

Parameter `input_is_ranks` can be used if inputs are rankings:

```
>>> data = otp.Ticks(X=[106, 100, 86, 101, 99, 103, 97, 113, 112, 110],
...                  Y=[7, 27, 2, 50, 28, 29, 20, 12, 6, 17])
>>> data = data.ranking('X').rename({'RANKING': 'RANKING_X'})
>>> data = data.ranking('Y').rename({'RANKING': 'RANKING_Y'})
>>> data = data.correlation_by_rank('RANKING_X', 'RANKING_Y', input_is_ranks=True)
>>> otp.run(data)
        Time  CORRELATION_BY_RANK
0 2003-12-04            -0.175758
```

##### SEE ALSO
**CORRELATION_BY_RANK** OneTick event processor
