# otp.Source.prevailing_price

#### ``Source.prevailing_price(quotes=None, , , input_field_name=None, output_field_name='VALUE', backfill_flag=True, bucket_interval=0, bucket_units=None, bucket_time='end', bucket_end_condition=None, boundary_tick_bucket='new', running=False)``

Computes prevailing security price using either:

* trade prices
* quote prices
* both trade and quote prices
* closing price from the previous business day.

If a time series of trades is the only input,
then the *latest trade price* is considered to be the prevailing price.
This time series must contain field **PRICE** or `input_field_name`.

If a time series of quotes is the only input,
then the *latest mid-quote price* is considered to be the prevailing price.
This time series must contain fields **ASK_PRICE** and **BID_PRICE** and be of tick type **QTE**.

If both trade and quote time series are the inputs,
then the latest mid-quote price is considered the prevailing price until the first trade tick arrives.
After the trade tick arrives, the price of the latest trade tick is considered the prevailing price.

Closing price may come from a symbol parameter **CLOSING_PRICE**.
Note that in order to be valid, this price must be adjusted for corporate actions
that happened between corresponding close and start time of the query.
If the previous day’s closing price is set,
it is considered to be the prevailing price at the start time of the query.

* **Parameters:**
  * **self** (``Source``) – The source of trades or quotes.
  * **quotes** (``Source``) – Optional source of quotes.
  * **input_field_name** (*str*) – The name of the input field with the price.
  * **output_field_name** (*str*) – The name of the output field with the resulting prevailing price.
  * **backfill_flag** (*bool*) – If set to True, the prevailing price at the query start time is assumed to be
    the price of the very first tick in this input time series.
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

Getting hourly prevailing price from trades only:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
>>> trd = trd.prevailing_price(bucket_interval=otp.Hour(1), output_field_name='PREVAIL')
>>> otp.run(trd, symbols='AAPL',
...         start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time   PREVAIL
0 2024-02-01 09:30:00  186.1100
1 2024-02-01 10:30:00  186.1100
2 2024-02-01 11:30:00  185.4000
3 2024-02-01 12:30:00  185.8957
4 2024-02-01 13:30:00  185.7350
5 2024-02-01 14:30:00  185.9781
6 2024-02-01 15:30:00  186.6512
7 2024-02-01 16:00:00  186.8312
```

Getting hourly prevailing price from quotes only:

```
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE')
>>> qte = qte.prevailing_price(bucket_interval=otp.Hour(1), output_field_name='PREVAIL')
>>> otp.run(qte, symbols='AAPL',
...         start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time  PREVAIL
0 2024-02-01 09:30:00  184.070
1 2024-02-01 10:30:00  186.000
2 2024-02-01 11:30:00  185.400
3 2024-02-01 12:30:00  188.000
4 2024-02-01 13:30:00  185.750
5 2024-02-01 14:30:00  185.975
6 2024-02-01 15:30:00  188.750
7 2024-02-01 16:00:00  186.895
```

Getting hourly prevailing price from trades and quotes:

```
>>> trd = otp.DataSource('US_COMP_SAMPLE', tick_type='TRD')
>>> qte = otp.DataSource('US_COMP_SAMPLE', tick_type='QTE')
>>> data = trd.prevailing_price(qte, bucket_interval=otp.Hour(1), output_field_name='PREVAIL')
>>> otp.run(data, symbols='AAPL',
...         start=otp.dt(2024, 2, 1, 9, 30), end=otp.dt(2024, 2, 1, 16), timezone='America/New_York')
                 Time   PREVAIL
0 2024-02-01 09:30:00  186.1100
1 2024-02-01 10:30:00  186.1100
2 2024-02-01 11:30:00  185.4000
3 2024-02-01 12:30:00  185.8957
4 2024-02-01 13:30:00  185.7350
5 2024-02-01 14:30:00  185.9781
6 2024-02-01 15:30:00  186.6512
7 2024-02-01 16:00:00  186.8312
```

##### SEE ALSO
**PREVAILING_PRICE** OneTick event processor
