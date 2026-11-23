# otp.ShowArchiveStats

### ``class ShowArchiveStats(, symbol=utils.adaptive, db=None, tick_type=utils.adaptive, start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

This event processor (EP) shows various stats about the queried symbol,
as well as an archive as a whole for each day within the queried interval.
Accelerator databases are not supported.
Memory databases will be ignored even within their life hours.
`TICK_SEARCH_MAX_DAY_BOUNDARY_OFFSET_SEC` is ignored by this event processor.

Output fields:

* **DATE** - the archive data date, as an integer in YYYYMMDD format.
  This field is returned only by OneTick builds since 20261102 and it’s not included in the schema.
* **COMPRESSION_TYPE** - archive compression type.
  In older archives native compression flag is not stored,
  so for example for gzip compression this field may say “GZIP or NATIVE_PLUS_GZIP”.
  The meta_data_upgrader.exe tool can be used to determine and inject that information in such cases
  in order to get a more precise result in this field.
* **TIME_RANGE_VALIDITY** - whether lowest and highest loaded timestamps (see below) are known.
  Like native compression flag, this information is missing in older archives
  and can be added using **meta_data_upgrader** tool.
* **LOWEST_LOADED_DATETIME** - the lowest loaded timestamp for the queried interval (across all symbols)
* **HIGHEST_LOADED_DATETIME** - the highest loaded timestamp for the queried interval (across all symbols)
* **TOTAL_TICKS** - the number of ticks for the queried interval (across all symbols).
  Also missing in older archives and can be added using **meta_data_upgrader**.
  If not available, -1 will be returned
* **SYMBOL_DATA_SIZE** - the size of the symbol in archive in bytes.
  This information is also missing in older archives, however the other options, it cannot later be added.
  In such cases -1 will be returned.
* **TOTAL_SYMBOLS** - the number of symbols for the queried interval
* **TOTAL_SIZE** - archive size in bytes for the queried interval
  (including the garbage potentially accumulated during appends).
* **ARCHIVE_MODIFICATION_TIME** - the latest modification time of the archive.

* **Parameters:**
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – Symbol(s) from which data should be taken.
    If set, will override the value specified in ``otp.run``.
  * **db** (*str* *,* *optional*) – 

    Database name to set on the OneTick’s graph node.

    The database must be set explicitly either in this parameter or in the symbols
    (parameter `symbol` or symbols of ``otp.run``).

    Note that this EP shows stats of the database set in this parameter
    even if the symbol has another database.
  * **tick_type** (*str*) – Tick type to set on the OneTick’s graph node.
    Default: ANY.
  * **start** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **end** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Show archive stats of the database for each day of the queried interval:

```
>>> data = otp.ShowArchiveStats(db='US_COMP_SAMPLE')
>>> df = otp.run(data, symbols='AAPL', start=otp.dt(2024, 2, 1), end=otp.dt(2024, 2, 6))
>>> df[['Time', 'COMPRESSION_TYPE', 'LOWEST_LOADED_DATETIME', 'HIGHEST_LOADED_DATETIME',
...     'TOTAL_TICKS', 'TOTAL_SYMBOLS']]
        Time  COMPRESSION_TYPE LOWEST_LOADED_DATETIME HIGHEST_LOADED_DATETIME  TOTAL_TICKS  TOTAL_SYMBOLS
0 2024-02-01  NATIVE_PLUS_GZIP             2024-02-01     2024-02-01 20:15:00    826170303           3308
1 2024-02-02  NATIVE_PLUS_GZIP             2024-02-02     2024-02-02 20:15:00    785761810           3289
2 2024-02-05  NATIVE_PLUS_GZIP             2024-02-05     2024-02-05 20:15:00    608045070           3315
```

Show archive stats of several databases at once
(the result is a dictionary with a dataframe for each symbol):

```
>>> data = otp.ShowArchiveStats()
>>> res = otp.run(data, symbols=['US_COMP_SAMPLE::AAPL', 'LSE_SAMPLE::VOD'],
...               start=otp.dt(2024, 2, 1, 12), end=otp.dt(2024, 2, 1, 13))
>>> res['US_COMP_SAMPLE::AAPL'][['Time', 'DATE', 'COMPRESSION_TYPE', 'TOTAL_SYMBOLS']]
                 Time      DATE  COMPRESSION_TYPE  TOTAL_SYMBOLS
0 2024-02-01 12:00:00  20240201  NATIVE_PLUS_GZIP           3308
>>> res['LSE_SAMPLE::VOD'][['Time', 'DATE', 'COMPRESSION_TYPE', 'TOTAL_SYMBOLS']]
                 Time      DATE          COMPRESSION_TYPE  TOTAL_SYMBOLS
0 2024-02-01 12:00:00  20240201  GZIP or NATIVE_PLUS_GZIP          61882
```

##### SEE ALSO
**SHOW_ARCHIVE_STATS** OneTick event processor

``onetick.py.db._inspection.DB.show_archive_stats()``

