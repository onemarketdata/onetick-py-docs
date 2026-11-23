# otp.ops.searched_case

### ``searched_case(*cases, default=None)``

Implements the logic of searched case statement in SQL.

Checks a list of condition expressions and returns matched result expression.

* **Parameters:**
  * **cases** (int | float | str | ``Operation``) – A list of condition-result pairs.
    Condition should be an ``Operation`` and result can be any supported type.
  * **default** (int | float | str | ``Operation``) – 

    Default result returned when no conditions are met.

    If not specified, default value by type is returned: 0 for numbers, empty strings for strings etc.
* **Return type:**
  ``Operation``

##### Examples

Basic example with one condition:

```
>>> data = otp.Ticks(X=[-1, 0, 1, 2])
>>> data['Y'] = otp.ops.searched_case(data['X'] > 0, 'POSITIVE')
>>> otp.run(data)
                     Time  X         Y
0 2003-12-01 00:00:00.000 -1
1 2003-12-01 00:00:00.001  0
2 2003-12-01 00:00:00.002  1  POSITIVE
3 2003-12-01 00:00:00.003  2  POSITIVE
```

Several conditions and `default` value can be specified:

```
>>> data = otp.Ticks(X=[-1, 0, 1, 2])
>>> data['Y'] = otp.ops.searched_case(
...     data['X'] > 0, 'POSITIVE',
...     data['X'] == 0, 'ZERO',
...     default='NEGATIVE',
... )
>>> otp.run(data)
                     Time  X         Y
0 2003-12-01 00:00:00.000 -1  NEGATIVE
1 2003-12-01 00:00:00.001  0      ZERO
2 2003-12-01 00:00:00.002  1  POSITIVE
3 2003-12-01 00:00:00.003  2  POSITIVE
```

##### SEE ALSO
**SEARCHED_CASE** OneTick function

``onetick.py.Source.if_else()``

``onetick.py.Source.apply()``

