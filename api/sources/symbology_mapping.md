# otp.SymbologyMapping

### ``class SymbologyMapping(dest_symbology=None, tick_type=utils.adaptive, start=utils.adaptive, end=utils.adaptive, symbols=utils.adaptive, schema=None, query_parameters=None, **kwargs)``

Bases: ``Source``

Shows symbology mapping information for specified securities stored in the reference database.

Input (source) symbology is taken from the input symbol,
if it has a symbology part in it (e.g., RIC::REUTERS::MSFT),
or defaults to that of the input database, which is specified in the locator file.

Parameter `symbol_date` must be set in ``otp.run``
for this source to work.

* **Parameters:**
  * **dest_symbology** (str, ``otp.param``) – Specifying the destination symbology for symbol translation.
  * **tick_type** (*str*) – 

    Tick type to set on the OneTick’s graph node.
    Can be used to specify database name with tick type or tick type only.

    By default setting this parameter is not required, database is usually set
    with parameter `symbols` or in ``otp.run``.
  * **start** – Custom start time of the source.
    If set, will override the value specified in ``otp.run``.
  * **end** – Custom end time of the source.
    If set, will override the value specified in ``otp.run``.
  * **symbols** – Symbol(s) from which data should be taken.
    If set, will override the value specified in ``otp.run``.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Getting mapping for OID symbology for one symbol:

```
>>> data = otp.SymbologyMapping(dest_symbology='OID')
>>> otp.run(data, symbols='US_COMP_SAMPLE::AAPL',  
...         symbol_date=otp.dt(2024, 2, 1),
...         date=otp.dt(2024, 2, 1))
        Time END_DATETIME MAPPED_SYMBOL_NAME
0 2024-02-01   2024-02-02               9706
```

Getting mapping for all symbols in US_COMP_SAMPLE database in single source:
