# otp.Source.time_filter

#### ``Source.time_filter(discard_on_match=False, start_time=0, end_time=0, day_patterns='', timezone=utils.default, end_time_tick_matches=False, inplace=False)``

Filters ticks by time.

* **Parameters:**
  * **discard_on_match** (*bool* *,* *optional*) – If `True`, then ticks that match the filter will be discarded.
    Otherwise, only ticks that match the filter will be passed.
  * **start_time** (str or int or ``datetime.time``, optional) – Start time of the filter, string must be in the format `HHMMSSmmm` or `HH:MM:SS[.mmm]`.
    Default value is 0.
  * **end_time** (str or int or ``datetime.time``, optional) – End time of the filter, string must be in the format `HHMMSSmmm` or `HH:MM:SS[.mmm]`.
    To filter ticks for an entire day, this parameter should be set to 24:00:00.
    Default value is 0.
  * **day_patterns** (*list* *or* *str*) – 

    Pattern or list of patterns that determines days for which the ticks can be propagated.
    A tick can be propagated if its date matches one or more of the patterns.
    Three supported pattern formats are:
    1. `month.week.weekdays`, 0 month means any month, 0 week means any week,
       : 6 week means the last week of the month for a given weekday(s),
         weekdays are digits for each day, 0 being Sunday.
    2. `month/day`, 0 month means any month.
    3. `year/month/day`, 0 year means any year, 0 month means any month.
  * **timezone** (*str* *,* *optional*) – Timezone of the filter.
    Default value is ``otp.config.tz``
    or timezone set in the parameter of ``otp.run``.
  * **end_time_tick_matches** (*bool* *,* *optional*) – If `True`, then the end time is inclusive.
    Otherwise, the end time is exclusive.
  * **inplace** (*bool* *,* *optional*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing. Otherwise method returns a new modified
    object. Default value is `False`.
  * **self** (*Source*)
* **Returns:**
  Returns `None` if `inplace=True`.
* **Return type:**
  ``Source`` or `None`

##### Examples

Filter ticks from 09:30:00 to 09:30:00.001:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']]
>>> data = data.time_filter(start_time='09:30:00', end_time='09:30:00.001')
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                            Time   PRICE  SIZE
0  2024-02-01 09:30:00.000961260  184.01   302
1  2024-02-01 09:30:00.000961491  184.00   100
2  2024-02-01 09:30:00.000961701  184.00     1
3  2024-02-01 09:30:00.000973163  184.00     1
4  2024-02-01 09:30:00.000973355  184.00     5
5  2024-02-01 09:30:00.000973517  184.00     5
6  2024-02-01 09:30:00.000973674  184.00     5
7  2024-02-01 09:30:00.000980967  184.00     1
8  2024-02-01 09:30:00.000984514  184.00    10
9  2024-02-01 09:30:00.000984626  184.00     1
10 2024-02-01 09:30:00.000984730  184.00     1
11 2024-02-01 09:30:00.000989008  184.00     1
12 2024-02-01 09:30:00.000992129  184.00     2
13 2024-02-01 09:30:00.000994257  184.00     2
14 2024-02-01 09:30:00.000994541  184.00     3
15 2024-02-01 09:30:00.000996695  184.00    10
16 2024-02-01 09:30:00.000999752  184.00   100
```

Filter ticks from 09:30:00 to 09:30:00.005 every Monday:

```
>>> data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='AAPL')
>>> data = data[['PRICE', 'SIZE']]
>>> data = data.time_filter(start_time='09:30:00', end_time='09:30:00.005', day_patterns='0.0.1')
>>> otp.run(data, start=otp.dt(2024, 2, 1), end=otp.dt(2024, 3, 1))
                           Time   PRICE  SIZE
0 2024-02-05 09:30:00.002470305  188.13    26
1 2024-02-05 09:30:00.003490655  188.15    26
2 2024-02-05 09:30:00.004413985  188.13     1
3 2024-02-12 09:30:00.004972167  188.41    50
4 2024-02-26 09:30:00.003312559  182.33   100
5 2024-02-26 09:30:00.003316234  182.33   100
```

##### SEE ALSO
**TIME_FILTER** OneTick event processor
