# otp.DbShowLoadedTimeRanges

### ``class DbShowLoadedTimeRanges(, use_cache=True, max_possible_loaded_date='today', prefer_speed_over_accuracy=False, symbol=utils.adaptive, db=utils.adaptive, tick_type='ANY', start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

For a specified database within the queried interval this event processor (EP) shows loaded tick time ranges:
start/end dates, start/end timestamps, number of loaded and total partitions
(the latter is important for virtual databases, for regular databases number of total partitions is always 1),
and `IS_MEMORY_DB` flag indicating whether interval is loaded from memory database or archive.

It shows the start date and end date and builds timestamps from these dates,
with zero hour, minute, and second and with database time zone.

It also does a boundary check, and if the loaded time range intersects with the queried interval,
while the query start date time is greater than the start range,
then the query start date and time will be shown.

Similarly, if the query end date and time is lesser than the end range,
the query end date and time will be shown.

If the date is not loaded, it will still be present in results, with `NUM_LOADED_PARTITIONS=0`.

If there is an intersection between memory and archive intervals,
the intersection is always considered part of memory db (`IS_MEMORY_DB=1`).

* **Parameters:**
  * **use_cache** (*bool*) – 

    If set to **True**, the event processor will use the cached results
    (see the `META_DATA_CACHE_FILE` in the Locator Variables documentation), if available.
    If the cache is available only up to some point,
    the rest of the data will be calculated and merged with the cache contents.
    If set to **False**, all the data will be recalculated even if the cache is available.
    Under no circumstances will the cache be updated.

    Default: **True**
  * **max_possible_loaded_date** (*str*) – 

    Possible values are `today` and `end_date`.
    If set to `today` (default), the dates in the future are not returned by this event processor.
    If set to `end_date`, returned ticks cover full time span of the query.

    Default: `today`
  * **prefer_speed_over_accuracy** (*bool*) – 

    If set to **True**, the event processor will use consider as loaded all days
    for which database’s archive directory, configured in the locator file,
    has a corresponding subdirectory with name in format YYYYMMDD,
    without checking whether that subdirectory has a file named index.
    The check for the existence of index file may be expensive, in terms of time it takes,
    when the file resides on NFS or on object storage, such as S3.

    Default: **False**
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – 

    Symbol name to bind to the OneTick’s graph node.

    Input symbols for the queries that involve this event processor
    should be of the form `<db_name>::` or `<db_name>::<some symbol name>`,
    so if parameter `db` is set, the symbol is bound as `<db>::<symbol>`,
    otherwise the symbol must contain the database name.

    If the value is not a string (e.g. ``Source``), it is used as is
    (so the symbols must contain the database name) and parameter `db` can’t be set.

    If neither `symbol` nor `db` is set,
    the symbols from ``otp.run`` are used.
  * **db** (*str*) – 

    Name of the database.
    It is bound to the OneTick’s graph node as a part of the symbol (`<db>::` or `<db>::<symbol>`),
    so symbols can’t be passed to ``otp.run`` if this parameter is set.

    If not set, the database should be specified in `symbol`
    or in the symbols of ``otp.run``.
  * **tick_type** (*str*) – 

    Tick type to set on the OneTick’s graph node.

    Default: `ANY`
  * **start** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **end** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Show loaded time ranges of the database:

```
>>> data = otp.DbShowLoadedTimeRanges(db='US_COMP_SAMPLE')
>>> data = data[['START_DATE', 'END_DATE', 'START_TIMESTAMP', 'END_TIMESTAMP', 'NUM_LOADED_PARTITIONS']]
>>> otp.run(data, start=otp.dt(2024, 2, 1), end=otp.dt(2024, 2, 8))
        Time  START_DATE  END_DATE START_TIMESTAMP END_TIMESTAMP  NUM_LOADED_PARTITIONS
0 2024-02-01    20240201  20240202      2024-02-01    2024-02-03                      1
1 2024-02-01    20240203  20240204      2024-02-03    2024-02-05                      0
2 2024-02-01    20240205  20240207      2024-02-05    2024-02-08                      1
```

The databases can also be set with the symbols in ``otp.run``,
e.g. to show loaded time ranges of several databases at once
(the result is a dictionary with a dataframe for each symbol):

```
>>> data = otp.DbShowLoadedTimeRanges()
>>> data = data[['START_DATE', 'END_DATE', 'NUM_LOADED_PARTITIONS']]
>>> res = otp.run(data, symbols=['US_COMP_SAMPLE::', 'LSE_SAMPLE::'],
...               start=otp.dt(2024, 2, 1), end=otp.dt(2024, 2, 6))
>>> res['US_COMP_SAMPLE::']
        Time  START_DATE  END_DATE  NUM_LOADED_PARTITIONS
0 2024-02-01    20240201  20240202                      1
1 2024-02-01    20240203  20240204                      0
2 2024-02-01    20240205  20240205                      1
>>> res['LSE_SAMPLE::']
        Time  START_DATE  END_DATE  NUM_LOADED_PARTITIONS
0 2024-02-01    20240201  20240206                      1
```

##### SEE ALSO
**DB/SHOW_LOADED_TIME_RANGES** OneTick event processor

``onetick.py.db._inspection.DB.dates()``

``onetick.py.db._inspection.DB.last_date``

