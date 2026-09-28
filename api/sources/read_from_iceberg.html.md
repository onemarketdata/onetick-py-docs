# otp.ReadFromIceberg

### ``class ReadFromIceberg(catalog_config=None, table_identifier=None, fields='', drop_fields=False, as_of_time=None, time_assignment='end', where='', symbology='', symbol_name_field='SYMBOL_NAME', batch_size=1000, symbol=utils.adaptive, db=utils.adaptive_to_default, tick_type=utils.adaptive, start=utils.adaptive, end=utils.adaptive, schema=None, query_parameters=None, **kwargs)``

Bases: ``Source``

Read ticks from an Iceberg table.

The table is specified by `table_identifier` and is accessed
with the catalog settings from the `catalog_config` file.

* **Parameters:**
  * **catalog_config** (*str*) – Path to a configuration file containing the Iceberg catalog parameters.
    For details on the file structure and how it is processed, see Examples below.
  * **table_identifier** (*str*) – The Iceberg table identifier, including the namespace and table name
    (for example, `namespace.tablename`).
  * **fields** (*list* *,* *str*) – A list of fields (`list` or comma-separated string) to be included in the output ticks.
    If not set, all available fields from the table are returned.
    See `drop_fields` parameter to propagate all fields except the listed ones.
  * **drop_fields** (*bool*) – If set to `True`, the fields listed in the `fields` parameter will not be propagated,
    and the fields that are not listed there will be propagated instead.
  * **as_of_time** (``otp.datetime``, ``datetime.datetime``, int) – Timestamp for the Iceberg time travel query.
    The table snapshot that was current as of this timestamp will be read,
    following the standard Iceberg time travel semantics.
    Integers are treated as the number of milliseconds since epoch.
    Datetime values without timezone are treated as values
    in ``otp.config.tz``.
  * **time_assignment** (*str*) – Timestamps of the ticks created by `ReadFromIceberg` are set to the start or to the end of the query
    depending on the `time_assignment` parameter.
    Possible values are `start` and `end` (for `_START_TIME` and `_END_TIME`).
  * **where** (*str*) – Specifies a criterion for selecting the rows to propagate.
    Wherever possible, Iceberg database predicate push-down is performed
    for certain sub-clauses of the specified expression.
  * **symbology** (*str*) – Symbology of the symbol names found in the `symbol_name_field` field.
    If specified, the reference database is used
    to find synonyms for the query symbols within this symbology.
  * **symbol_name_field** (*str*) – Field that is expected to contain the symbol name.
    When this parameter is set and specific symbols are bound to the query,
    only rows matching those symbols are propagated.
    If multiple symbols are present,
    rows are routed to the appropriate sub-queries based on this field’s value.
  * **batch_size** (*int*) – The maximum number of rows to be collected in the Java layer
    before they are transferred to the C++ layer.
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – Symbol(s) from which data should be taken.
  * **tick_type** (*str*) – Tick type.
    Default: ANY.
  * **start** (``otp.datetime``) – Start time for tick generation. By default the start time of the query will be used.
  * **end** (``otp.datetime``) – End time for tick generation. By default the end time of the query will be used.
  * **schema** (*dict*) – 

    Set the schema of the python ``Source`` object of this class.

    Schema can’t be automatically derived from the Iceberg table, so it should be set
    manually for Python-level type checking to work.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.
  * **kwargs** – Deprecated. Use `schema` instead.
    Dictionary of columns names with their types.

#### NOTE
This EP is supported only on OneTick for 64-bit Windows/Linux platforms.

This source requires Java 17 or higher to be installed.
Also Java library path should be added to **PATH** (Windows) or **LD_LIBRARY_PATH** (Linux)
environment variables and to **OMD_JAVALIBPATH** OneTick config variable.

##### Examples

Write Iceberg catalog configuration first:

```
>>> with open('catalog.cfg', 'w') as f:
...     f.write('''
...         catalog.name=rest_catalog
...         type=rest
...         uri=http://localhost:8181
...         warehouse=s3://warehouse/
...         s3.region=us-east-1
...         client.region=us-east-1
...         s3.path-style-access=true
...         s3.access-key-id=admin
...         s3.secret-access-key=password
...         io-impl=org.apache.iceberg.aws.s3.S3FileIO
...         s3.delete.enabled=true
...         s3.acceleration-enabled=false
...     ''')
```

Then read all fields from the table:

```
>>> data = otp.ReadFromIceberg(catalog_config='catalog.cfg',
...                            table_identifier='exchange.trades')
>>> otp.run(data)
```

Read only the fields you need:

```
>>> data = otp.ReadFromIceberg(catalog_config='catalog.cfg',
...                            table_identifier='exchange.trades',
...                            fields=['PRICE', 'SIZE'])
>>> otp.run(data)
```

Propagate all fields except the listed ones:

```
>>> data = otp.ReadFromIceberg(catalog_config='catalog.cfg',
...                            table_identifier='exchange.trades',
...                            fields=['SIZE'],
...                            drop_fields=True)
>>> otp.run(data)
```

Filter rows and set tick timestamps from the `trade_time` field:

```
>>> data = otp.ReadFromIceberg(catalog_config='catalog.cfg',
...                            table_identifier='exchange.trades',
...                            fields=['PRICE', 'SIZE', 'trade_time'],
...                            time_assignment='trade_time',
...                            where='PRICE > 20')
>>> otp.run(data)
```

Read the table snapshot that was current at the specified point in time:

```
>>> data = otp.ReadFromIceberg(catalog_config='catalog.cfg',
...                            table_identifier='exchange.trades',
...                            fields=['PRICE', 'SIZE'],
...                            as_of_time=otp.datetime(2023, 1, 1, 12))
>>> otp.run(data)
```

##### SEE ALSO
**READ_FROM_ICEBERG** OneTick event processor

``onetick.py.Source.write_iceberg()``

