# otp.DbShowConfig

### ``class DbShowConfig(, db_name=None, config_type='locator_entry', symbol=utils.adaptive, db=utils.adaptive, tick_type='ANY', start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Shows the specified configuration for a database.

* **Parameters:**
  * **db_name** (*str* *,* *optional*) – 

    Specifies the database name to get the configuration for.
    If not specified, the database name is extracted from the bound symbol.

    And if the database specified in this parameter is not available there, OneTick may return exception.
  * **config_type** (*str*) – 

    `db_time_intervals`, `locator_entry` (default).

    If `locator_entry` is specified, a string representing db’s locator entry along with `VDB_FLAG`
    (this flag equals 1 when the database is virtual and 0 otherwise) will be returned.

    If `db_time_intervals` is specified, then time intervals configured in the locator file
    will be propagated including additional information, such as `LOCATION`, `ARCHIVE_DURATION`,
    `DAY_BOUNDARY_TZ`, `DAY_BOUNDARY_OFFSET`, `ALTERNATIVE_LOCATIONS`, etc.
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – 

    Symbol name to bind to the OneTick’s graph node.

    If parameter `db_name` is not specified, this event processor takes the database only from the symbol,
    so the symbols should be of the form `<db_name>::` or `<db_name>::<some symbol name>`.
    If parameter `db` is set, the symbol is bound as `<db>::<symbol>`,
    otherwise the symbol must contain the database name.

    If the value is not a string (e.g. ``Source``), it is used as is
    (so the symbols must contain the database name) and parameter `db` can’t be set.

    If neither `symbol` nor `db` is set,
    the symbols from ``otp.run`` are used.
  * **db** (*str* *,* *optional*) – 

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

Show locator entry of the database:

```
>>> data = otp.DbShowConfig()
>>> df = otp.run(data, symbols='US_COMP_SAMPLE::', start=otp.dt(2024, 1, 2), end=otp.dt(2024, 1, 3))
>>> print(df['LOCATOR_STRING'][0])
<DB ARCHIVE_COMPRESSION_TYPE="NATIVE_PLUS_GZIP" ... ID="US_COMP_SAMPLE" ...>
    <LOCATIONS >
        <LOCATION ACCESS_METHOD="file" ... END_TIME="20380101000000" ... START_TIME="20240101000000" />
    </LOCATIONS>
</DB>
```

The database can also be set with parameter `db`,
e.g. show time intervals configured in the locator for the database:

```
>>> data = otp.DbShowConfig(config_type='db_time_intervals', db='US_COMP_SAMPLE')
>>> df = otp.run(data, start=otp.dt(2024, 1, 2), end=otp.dt(2024, 1, 3))
>>> df
        Time     START_DATE       END_DATE  GROWABLE_ARCHIVE_FLAG  ARCHIVE_DURATION ... DAY_BOUNDARY_TZ ...
0 2024-01-02  1704067200000  2145916800000                      0                 0 ...         EST5EDT ...
```

Show time intervals of several databases at once
(the result is a dictionary with a dataframe for each symbol):

```
>>> data = otp.DbShowConfig(config_type='db_time_intervals')
>>> data = data[['START_DATE', 'END_DATE', 'DAY_BOUNDARY_TZ']]
>>> res = otp.run(data, symbols=['US_COMP_SAMPLE::', 'LSE_SAMPLE::'],
...               start=otp.dt(2024, 1, 2), end=otp.dt(2024, 1, 3))
>>> res['US_COMP_SAMPLE::']
        Time     START_DATE       END_DATE DAY_BOUNDARY_TZ
0 2024-01-02  1704067200000  2145916800000         EST5EDT
>>> res['LSE_SAMPLE::']
        Time  START_DATE       END_DATE DAY_BOUNDARY_TZ
0 2024-01-02           0  2145916800000             GMT
```

##### SEE ALSO
**DB/SHOW_CONFIG** OneTick event processor

``onetick.py.db._inspection.DB.show_config()``.

