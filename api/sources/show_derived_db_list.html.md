# otp.ShowDerivedDbList

### ``class ShowDerivedDbList(, db_discovery_scope='query_host_only', time_range='configured_time_interval', selection_criteria='all', symbol=utils.adaptive, db=utils.adaptive, tick_type='ANY', start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Shows the list of derived databases.

Output: A list of derived databases, represented in base_db_name//derived_db_name format.
Database names in the output are unique.
Will skip processing of directories which have <.tmp> extension.

* **Parameters:**
  * **db_discovery_scope** (*str*) – 

    `query_host_and_all_reachable_hosts`, `query_host_only` (default).

    When `query_host_and_all_reachable_hosts` is specified,
    an attempt will be performed to get derived databases from all hosts reachable from the process
    (it could be a client process, or could be a tick server, depending on where a queried symbol resides)
    where the query containing this event processor is executed.

    When `query_host_only` is specified,
    only derived databases from the host on which the query is performed will be returned.
  * **time_range** (*str*) – 

    `configured_time_interval` (default), `query_time_interval`.

    When `configured_time_interval` is specified,
    an attempt will be performed to get all possible derived databases.

    When `query_time_interval` is specified,
    only derived databases that have data/raw data within the specified query time interval will be returned.
  * **selection_criteria** (*str*) – Possible values are `all`, `derived_from_current_db` and `direct_children_of_current_db`.
    Default value is `all`.
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – 

    Symbol name to bind to the OneTick’s graph node.

    The database of the symbol is the current (parent) database for `selection_criteria`
    and it also defines the process where the query is executed.
    The symbols should be of the form `<db_name>::` or `<db_name>::<some symbol name>`,
    so if parameter `db` is set, the symbol is bound as `<db>::<symbol>`,
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

    This database is the current (parent) database for `selection_criteria`,
    so if `selection_criteria` is not `all`, it must be set in this parameter or in the symbols.
    A warning is shown if neither this parameter nor `symbol` is set in this case.
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

Let’s create a derived database and a database derived from it:

```
>>> db = otp.DB('WRITE_DB//DERIVED')
>>> session.use(db)
>>> db.add(otp.Ticks(A=[1]))
>>> db_2x = otp.DB('WRITE_DB//DERIVED//DERIVED_2X')
>>> session.use(db_2x)
>>> db_2x.add(otp.Ticks(A=[1]))
```

Get the list of all databases derived from the database:

```
>>> data = otp.ShowDerivedDbList(selection_criteria='derived_from_current_db', db='WRITE_DB')
>>> otp.run(data)
        Time                DERIVED_DB_NAME
0 2003-12-01              WRITE_DB//DERIVED
1 2003-12-01  WRITE_DB//DERIVED//DERIVED_2X
```

Get the list of direct children of the database:

```
>>> data = otp.ShowDerivedDbList(selection_criteria='direct_children_of_current_db', db='WRITE_DB')
>>> otp.run(data)
        Time    DERIVED_DB_NAME
0 2003-12-01  WRITE_DB//DERIVED
```

##### SEE ALSO
**SHOW_DERIVED_DB_LIST** OneTick event processor

``onetick.py.derived_databases()``

``otp.ShowDbList``

