# otp.ShowSymbologyList

### ``class ShowSymbologyList(symbol=utils.adaptive, db=utils.adaptive_to_default, tick_type=utils.adaptive, start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Lists local symbologies and symbologies from directly or indirectly attached tick servers.

Output ticks have `SYMBOLOGY` field with the name of the symbology.

* **Parameters:**
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – Symbol(s) from which data should be taken.
    If set, will override the value specified in ``otp.run``.
  * **db** (*str*) – Database name to set on the OneTick’s graph node.
    By default ``otp.config.default_db`` is used.
  * **tick_type** (*str*) – Tick type to set on the OneTick’s graph node.
    Default: ANY.
  * **start** (``otp.datetime``) – Custom start time of the source.
    If set, will override the value specified in ``otp.run``.
  * **end** (``otp.datetime``) – Custom end time of the source.
    If set, will override the value specified in ``otp.run``.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

List all available symbologies:

```
>>> src = otp.ShowSymbologyList()
>>> otp.run(src)
        Time SYMBOLOGY
0 2003-12-01       BBG
1 2003-12-01      BSYM
2 2003-12-01      BTKR
...
```

##### SEE ALSO
**SHOW_SYMBOLOGY_LIST** OneTick event processor

``onetick.py.SymbologyMapping``

``onetick.py.misc.get_symbology_mapping()``

