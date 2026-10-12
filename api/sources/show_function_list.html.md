# otp.ShowFunctionList

### ``class ShowFunctionList(symbol=None, tick_type=None, start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Returns the list of functions and their parameter.

One tick is generated for each parameter of each function.

If a function does not have parameters, only one tick is propagated with field **HAS_PARAMETERS** set to false.
In this case, numeric fields that are describing parameters, take the value 0
(except for PARAMETER_TYPE, which takes -1) and string fields take empty string.

* **Parameters:**
  * **symbol** (*str*) – Bound symbol on the node of the graph.
    Not set by default – the value from ``otp.run`` will be used.
  * **tick_type** (*str*) – Tick type set on the node of the graph.
    Not set by default.
  * **start** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **end** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Get the list of all OneTick functions:

```
>>> data = otp.ShowFunctionList()
>>> otp.run(data, symbols='LOCAL::')
          Time                   FUNCTION_NAME PARAMETER_NAME  ... PARAMETER_TYPE_NAME  ...
0   2003-12-01                             ABS         NUMBER  ...             DECIMAL  ...
1   2003-12-01      DYNAMIC_TICK.GET_TIMESTAMP                 ...                      ...
2   2003-12-01               AS_YYYYMMDDHHMMSS           TIME  ...         TIME_MSEC64  ...
3   2003-12-01               AS_YYYYMMDDHHMMSS       TIMEZONE  ...              STRING  ...
4   2003-12-01                        NSECTIME           TIME  ...         TIME_NSEC64  ...
..         ...                             ...            ...  ...                 ...  ...
```
