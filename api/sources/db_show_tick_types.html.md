# otp.DbShowTickTypes

### ``class DbShowTickTypes(, use_cache=True, show_schema=False, schemas_to_show='union_of_fields', include_memdb=True, symbol=utils.adaptive, db=utils.adaptive, tick_type='ANY', start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Shows tick types for a specified database.

* **Parameters:**
  * **use_cache** (*bool*) – 

    If set to **True**, the event processor will use the cached results
    (see the `META_DATA_CACHE_FILE` description in the OneTick Installation and Administration Guide)
    if available.
    If the cache is available only up to some point,
    the rest of the data will be calculated and merged with the cache contents.
    If set to **False**, all the data will be re-calculated even if cache is available.
    Under no circumstances will the cache be updated.

    Default: **True**
  * **show_schema** (*bool*) – 

    If set to **True**, for each tick type its schema will be shown (names, types and sizes of fields).

    Default: **False**
  * **schemas_to_show** (*str*) – 

    Have an effect only if `show_schema` is **True**.
    If set to `union_of_fields`, only one of the occurrence of the field with its type is displayed
    for whatever field name ever was for that tick type.
    When set to `each_schema`, each field for a given tick type is displayed
    as many times as it appears in schemas. Indexing of various schemes is performed.
    It is possible that the same field will have different types for different dates.

    Default: `union_of_fields`
  * **include_memdb** (*bool*) – 

    Setting this parameter to **True** will return result from memory databases too.
    Otherwise only the archive databases will be used.

    Default: **True**
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

Show tick types of the database:

```
>>> data = otp.DbShowTickTypes(db='US_COMP_SAMPLE')
>>> df = otp.run(data, start=otp.dt(2024, 2, 1), end=otp.dt(2024, 2, 2))
>>> df
        Time TICK_TYPE_NAME
0 2024-02-01            DAY
1 2024-02-01            IND
2 2024-02-01           LULD
...
```

Show tick types of the database with their schemas:

```
>>> data = otp.DbShowTickTypes(show_schema=True, db='US_COMP_SAMPLE')
>>> data = data[['TICK_TYPE_NAME', 'FIELD_NAME', 'FIELD_TYPE_NAME', 'FIELD_SIZE']]
>>> otp.run(data, start=otp.dt(2024, 2, 1), end=otp.dt(2024, 2, 2))
          Time TICK_TYPE_NAME   FIELD_NAME   FIELD_TYPE_NAME  FIELD_SIZE
0   2024-02-01            DAY        CLOSE       TYPE_DOUBLE           8
1   2024-02-01            DAY     EXCHANGE       TYPE_STRING           4
2   2024-02-01            DAY         HIGH       TYPE_DOUBLE           8
...
```

The databases can also be set with the symbols in ``otp.run``,
e.g. to show tick types of several databases at once
(the result is a dictionary with a dataframe for each symbol):

```
>>> data = otp.DbShowTickTypes()
>>> res = otp.run(data, symbols=['US_COMP_SAMPLE::', 'LSE_SAMPLE::'],
...               start=otp.dt(2024, 2, 1), end=otp.dt(2024, 2, 2))
>>> {symbol: list(df['TICK_TYPE_NAME']) for symbol, df in res.items()}
{'US_COMP_SAMPLE::': ['DAY', 'IND', 'LULD', 'MKT', 'NBBO', 'QTE', 'STAT', 'TRD'],
 'LSE_SAMPLE::': ['DAY', 'IND', 'MKT', 'PRL_FULL', 'QTE', 'STAT', 'TRD']}
```

##### SEE ALSO
**DB/SHOW_TICK_TYPES** OneTick event processor

``onetick.py.db._inspection.DB.tick_types()``

``onetick.py.db._inspection.DB.schema()``

