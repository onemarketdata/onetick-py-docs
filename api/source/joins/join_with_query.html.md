# otp.Source.join_with_query

#### ``Source.join_with_query(query, how='outer', symbol=None, params=None, start=None, end=None, timezone=None, prefix=None, caching=None, keep_time=None, where=None, default_fields_for_outer_join=None, symbol_time=None, concurrency=None, batch_size=None, shared_thread_count=None, process_query_async=True, **kwargs)``

For each tick executes `query`.

* **Parameters:**
  * **query** (*callable* *,* *Source*) – 

    Callable `query` should return ``Source``. This object will be evaluated by OneTick (not python)
    for every tick. Note python code will be executed only once, so all python’s conditional expressions
    will be evaluated only once too.
    Callable should have `symbol` parameter and the parameters with names
    from `params` if they are specified in this method.

    If `query` is a ``Source`` object then it will be propagated as a query to OneTick.
  * **how** ( *'inner'* *,*  *'outer'*) – Type of join. If **inner**, then each tick is propagated
    only if its `query` execution has a non-empty result.
  * **params** (*dict*) – Mapping of the parameters’ names and their values for the `query`.
    ``Columns`` can be used as a value.
  * **symbol** (*str* *,* *Operation* *,* *dict* *,* *Source* *, or* *tuple* ***Union* *[*[*str* *,* *Operation* *]* *,* *Union* **[*dict* *,* *Source* *]* *]*) – 

    Symbol name to use in `query`. In addition, symbol params can be passed along with symbol name.

    Symbol name can be passed as a string or as an ``Operation``.

    Symbol parameters can be passed as a dictionary. Also, the main ``Source`` object,
    or the object containing a symbol parameter list, can be used as a list of symbol parameter.
    Special symbol parameters (\_PARAM_START_TIME_NANOS and \_PARAM_END_TIME_NANOS)
    will be ignored and will not be propagated to `query`.

    `symbol` will be interpreted as a symbol name or as symbol parameters, depending on its type.
    You can pass both as a tuple.

    If symbol name is not passed, then symbol name from the main source is used.
  * **start** (``otp.datetime``, ``otp.Operation``) – Start time of `query`.
    By default, start time of the main source is used.
  * **end** (``otp.datetime``, ``otp.Operation``) – End time of `query` (note that it’s non-inclusive).
    By default, end time of the main source is used.
  * **start_time** – 

    #### Deprecated
    Deprecated since version 1.48.4: The same as `start`.
  * **end_time** – 

    #### Deprecated
    Deprecated since version 1.48.4: The same as `end`.
  * **timezone** (*Optional* *,* *str*) – Timezone of `query`.
    By default, timezone of the main source is used.
  * **prefix** (*str*) – Prefix for the names of joined tick fields.
  * **caching** (*str*) – 

    If None caching is disabled (default). You can specify caching by using values:
    > * ’cross_symbol’: cache is the same for all symbols
    > * ’per_symbol’: cache is different for each symbol.

    #### NOTE
    When parameter `process_query_async` is set to `True` (default), caching may work
    unexpectedly, because ticks will be accumulated in batches and `query` will be processed
    in different threads.
  * **keep_time** (*str*) – Name for the joined timestamp column. None means no timestamp column will be joined.
  * **where** (*Operation*) – Condition to filter ticks for which the result of the `query` will be joined.
  * **default_fields_for_outer_join** (*dict*) – When you use outer join, all output ticks will have fields from the schema of the joined source.
    If nothing was joined to a particular output tick, these fields will have default values for their type.
    This parameter allows to override the values that would be added to ticks for which nothing was joined.
    Dictionary keys should be field names, and dictionary values should be constants
    or ``Operation`` expressions
  * **symbol_time** (``otp.datetime``, ``otp.Operation``) – Time that will be used by Onetick to map the symbol with which `query` is executed to the reference data.
    This parameter is only necessary if the query is expected to perform symbology conversions.
  * **concurrency** (*int*) – Specifies concurrency for the joined `query` execution.
    Default is 1 (no concurrency).
  * **batch_size** (*int*) – Specifies batch size for the joined `query` execution. Default is 0.
  * **shared_thread_count** (*int*) – Specifies number of threads for asynchronous processing of `query` per unbound symbol list.
    By default, the number of threads is 1.
  * **process_query_async** (*bool*) – 

    Switches between synchronous and asynchronous execution of queries.

    While asynchronous execution is generally much more effective,
    in certain cases synchronous execution may still be preferred
    (e.g., when there are a few input ticks, each initiating a memory-consuming query).

    In asynchronous mode typically while parallel thread is processing the query,
    EP accumulates some input ticks.
  * **self** (*Source*)
* **Returns:**
  Source with joined ticks from `query`
* **Return type:**
  ``Source``

##### Examples

```
>>> joined = otp.Ticks(Y=[-1])
>>> joined = joined.update(dict(Y=1), where=(joined.Symbol.name == 'a'))
>>> data = otp.Ticks(X=[1, 2],
...                  S=['a', 'b'])
>>> data = data.join_with_query(joined, how='inner', symbol=data['S'])
>>> otp.run(data)
                     Time  Y  X  S
0 2003-12-01 00:00:00.000  1  1  a
1 2003-12-01 00:00:00.001 -1  2  b
```

```
>>> joined = otp.Ticks(ADDED=[-1])
>>> joined = joined.update({'ADDED': 1}, where=(joined.Symbol.name == '3'))  # symbol name is always string
>>> data = otp.Ticks(A=[1, 2], B=[2, 4])
>>> data = data.join_with_query(joined, how='inner', symbol=(data['A'] + data['B']))
>>> otp.run(data)
                     Time  ADDED  A  B
0 2003-12-01 00:00:00.000      1  1  2
1 2003-12-01 00:00:00.001     -1  2  4
```

Constants as symbols are also supported:

```
>>> joined = otp.Ticks(ADDED=[otp.Source.Symbol.name])
>>> data = otp.Ticks(A=[1, 2], B=[2, 4])
>>> data = data.join_with_query(joined, how='inner', symbol='XX')
>>> otp.run(data)
                     Time ADDED  A  B
0 2003-12-01 00:00:00.000    XX  1  2
1 2003-12-01 00:00:00.001    XX  2  4
```

Function object as query is also supported (Note it will be executed only once in python’s code):

```
>>> def func(symbol):
...     t = otp.Ticks(TYPE=['six'])
...     t = t.update(dict(TYPE='three'), where=(symbol.name == '3'))  # symbol is always converted to string
...     t['TYPE'] = symbol['PREF'] + t['TYPE'] + symbol['POST']
...     return t
>>> data = otp.Ticks(A=[1, 2], B=[2, 4])
>>> data = data.join_with_query(func, how='inner', symbol=(data['A'] + data['B'], dict(PREF='_', POST='$')))
>>> otp.run(data)
                     Time     TYPE  A  B
0 2003-12-01 00:00:00.000  _three$  1  2
1 2003-12-01 00:00:00.001    _six$  2  4
```

It’s possible to pass the source itself as a list of symbol parameters, which will make all of its fields
accessible through the `symbol` object:

```
>>> def func(symbol):
...     t = otp.Ticks(TYPE=['six'])
...     t['TYPE'] = symbol['PREF'] + t['TYPE'] + symbol['POST']
...     return t
>>> data = otp.Ticks(A=[1, 2], B=[2, 4], PREF=['_', '$'], POST=['$', '_'])
>>> data = data.join_with_query(func, how='inner', symbol=data)
>>> otp.run(data)
                     Time   TYPE  A  B PREF POST
0 2003-12-01 00:00:00.000  _six$  1  2    _    $
1 2003-12-01 00:00:00.001  $six_  2  4    $    _
```

The examples above can be rewritten by using onetick query parameters instead of symbol parameters.
OTQ parameters are global for query, while symbol parameters can be redefined by bound symbols:

```
>>> def func(symbol, pref, post):
...     t = otp.Ticks(TYPE=['six'])
...     t = t.update({'TYPE': 'three'}, where=(symbol.name == '3'))  # symbol is always converted to string
...     t['TYPE'] = pref + t['TYPE'] + post
...     return t
>>> data = otp.Ticks(A=[1, 2], B=[2, 4])
>>> data = data.join_with_query(func, how='inner', symbol=(data['A'] + data['B']),
...                             params={'pref': '_', 'post': '$'})
>>> otp.run(data)
                     Time     TYPE  A  B
0 2003-12-01 00:00:00.000  _three$  1  2
1 2003-12-01 00:00:00.001    _six$  2  4
```

Some or all onetick query parameters can be column or expression also:

```
>>> def func(symbol, pref, post):
...     t = otp.Ticks(TYPE=['six'])
...     t = t.update({'TYPE': 'three'}, where=(symbol.name == '3'))  # symbol is always converted to string
...     t['TYPE'] = pref + t['TYPE'] + post
...     return t
>>> data = otp.Ticks(A=[1, 2], B=[2, 4], PREF=['^', '_'], POST=['!', '$'])
>>> data = data.join_with_query(func, how='inner', symbol=(data['A'] + data['B']),
...                             params={'pref': data['PREF'] + '.', 'post': data['POST']})
>>> otp.run(data)
                     Time      TYPE  A  B PREF POST
0 2003-12-01 00:00:00.000  ^.three!  1  2    ^    !
1 2003-12-01 00:00:00.001    _.six$  2  4    _    $
```

You can specify `start` and `end` time of the query, otherwise time interval of the main query will be used:

```
>>> joined = otp.Ticks(Y=[1, 2])
>>> data = otp.Ticks(X=[1, 2])
>>> data = data.join_with_query(joined, how='inner',
...                             start=otp.dt(2003, 12, 1, 0, 0, 0, 1000),
...                             end=otp.dt(2003, 12, 1, 0, 0, 0, 3000))
>>> otp.run(data)
                     Time  Y  X
0 2003-12-01 00:00:00.000  1  1
1 2003-12-01 00:00:00.000  2  1
2 2003-12-01 00:00:00.001  1  2
3 2003-12-01 00:00:00.001  2  2
```

By default joined query inherits start and end time from the main query:

```
>>> joined_query = otp.Tick(JOINED_START_TIME=otp.meta_fields.start_time,
...                         JOINED_END_TIME=otp.meta_fields.end_time)
>>> main_query = otp.Tick(A=1)
>>> data = main_query.join_with_query(joined_query)
>>> otp.run(data, start=otp.dt(2003, 12, 1), end=otp.dt(2003, 12, 4))
        Time JOINED_START_TIME JOINED_END_TIME  A
0 2003-12-01        2003-12-01      2003-12-04  1
```

Parameters `start` and `end` can be used to change time interval for the joined query:

```
>>> data = main_query.join_with_query(joined_query, start=otp.dt(2024, 1, 1), end=otp.dt(2024, 1, 3))
>>> otp.run(data, start=otp.dt(2003, 12, 1), end=otp.dt(2003, 12, 4))
        Time JOINED_START_TIME JOINED_END_TIME  A
0 2003-12-01        2024-01-01      2024-01-03  1
```

Note that query `start` time is inclusive, but query `end` time is not,
meaning that ticks with timestamps equal to the query end time will not be included:

```
>>> main_query = otp.Tick(A=1)
>>> joined_query = otp.Tick(DAY=0, bucket_interval=24*60*60)
>>> joined_query['DAY'] = joined_query['TIMESTAMP'].dt.day_of_month()
>>> otp.run(joined_query, start=otp.dt(2003, 12, 1), end=otp.dt(2003, 12, 5))
        Time  DAY
0 2003-12-01    1
1 2003-12-02    2
2 2003-12-03    3
3 2003-12-04    4
```

```
>>> joined_query = joined_query.last()
>>> data = main_query.join_with_query(joined_query,
...                                   start=otp.dt(2003, 12, 1), end=otp.dt(2003, 12, 4))
>>> otp.run(data)
        Time  DAY  A
0 2003-12-01    3  1
```

If you want to include such ticks, you can add one nanosecond to the query end time:

```
>>> data = main_query.join_with_query(joined_query,
...                                   start=otp.dt(2003, 12, 1), end=otp.dt(2003, 12, 4) + otp.Nano(1))
>>> otp.run(data)
        Time  DAY  A
0 2003-12-01    4  1
```

Use `keep_time` parameter to keep or rename original timestamp column:

```
>>> d = otp.Ticks(Y=[1, 2])
>>> data = otp.Ticks(X=[1, 2])
>>> res = data.join_with_query(d, how='inner', keep_time="ORIG_TIME")
>>> otp.run(res)
                     Time  Y               ORIG_TIME  X
0 2003-12-01 00:00:00.000  1 2003-12-01 00:00:00.000  1
1 2003-12-01 00:00:00.000  2 2003-12-01 00:00:00.001  1
2 2003-12-01 00:00:00.001  1 2003-12-01 00:00:00.000  2
3 2003-12-01 00:00:00.001  2 2003-12-01 00:00:00.001  2
```

##### SEE ALSO
**JOIN_WITH_QUERY** OneTick event processor
