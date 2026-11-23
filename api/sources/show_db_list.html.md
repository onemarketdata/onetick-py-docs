# otp.ShowDbList

### ``class ShowDbList(, cep_only=False, show_description=False, symbol=utils.adaptive, db=utils.adaptive, tick_type=utils.adaptive, start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Returns a list of all databases visible from the process
(it could be a client process, or could be a tick server, depending on where a queried symbol resides)
where the query containing this event processor is executed.
Those databases are specified in the locator file explicitly or are auto-discovered,
by the above-mentioned process.

Output: One tick for each database.

#### NOTE
Some OneTick builds may return additional fields not listed in the schema of this source,
e.g. **REF_DATA_DB**.

* **Parameters:**
  * **cep_only** (*bool*) – 

    If set to **True**, only CEP databases will be returned.

    Default: **False**
  * **show_description** (*bool*) – 

    If set to **True** the output will also include the database’s description, in the field `DESCRIPTION`

    Default: **False**
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – Symbol(s) from which data should be taken.
    If set, will override the value specified in ``otp.run``.
  * **db** (*str*) – 

    Database name to set on the OneTick’s graph node.
    By default ``otp.config.default_db`` is used.

    The database of the symbol defines the process where the query is executed
    (e.g. for a database located on a remote tick server only the databases of this tick server are returned).
  * **tick_type** (*str*) – Tick type to set on the OneTick’s graph node.
    Default: ANY.
  * **start** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **end** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Get the list of all available databases:

```
>>> data = otp.ShowDbList()
>>> data = data[['DATABASE_NAME', 'SYMBOLOGY', 'START_TIME', 'END_TIME']]
>>> otp.run(data)
          Time    DATABASE_NAME    SYMBOLOGY     START_TIME       END_TIME
0   2003-12-01               A3         DTKR              0  2145916800000
1   2003-12-01         A3_DAILY         DTKR              0  2145916800000
2   2003-12-01            ABAXX        ABAXX              0  2145916800000
...
```

Get only CEP databases:

```
>>> data = otp.ShowDbList(cep_only=True)
>>> data = data[['DATABASE_NAME', 'SYMBOLOGY', 'START_TIME', 'END_TIME']]
>>> otp.run(data)
        Time DATABASE_NAME SYMBOLOGY    START_TIME       END_TIME
0 2003-12-01        COMMON       BZX  975628800000  1919653200000
1 2003-12-01       DEMO_L1       BZX  975628800000  1919653200000
```

The database set in `db` parameter defines the process where the query is executed.
For example, the local database `WRITE_DB` is visible from the client process,
but not from the remote tick server where the database `US_COMP_SAMPLE` resides:

```
>>> df = otp.run(otp.ShowDbList(db='WRITE_DB'))
>>> 'WRITE_DB' in set(df['DATABASE_NAME'])
True
>>> df = otp.run(otp.ShowDbList(db='US_COMP_SAMPLE'), start=otp.dt(2024, 2, 1), end=otp.dt(2024, 2, 2))
>>> 'WRITE_DB' in set(df['DATABASE_NAME'])
False
```

##### SEE ALSO
**SHOW_DB_LIST** OneTick event processor

``onetick.py.databases()``

``otp.AccessInfo``

