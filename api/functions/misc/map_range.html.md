# otp.ops.map_range

### ``map_range(value, , ranges, , default=None)``

Maps specified numeric `value` to one of the ranges specified in `ranges`
and returns the label of the mapped range.

* **Parameters:**
  * **value** (int | ``Operation``) – Numeric value to map.
  * **ranges** (*dict* **[*str* *|* *int* *,* *tuple* **[*int* *,* *int* *]* *]*) – 

    Ranges to map the `value`.
    It is a mapping from range labels (numbers or string) to ranges (tuples range start and range end)

    It is not allowed to have mixed types of labels. They must either all be strings or all be integers.

    The ranges must not be overlapping, but do not have to be continuous.
  * **default** (*int* *|* *str*) – This default value will be used if the `value` didn’t match any range.
    By default the default value by type will be used: 0 for numbers and empty string for strings.
* **Return type:**
  ``Operation``

##### Examples

Map the value to two ranges and return string labels:

```
>>> data = otp.Ticks(HOUR=list(range(0, 25, 3)))
>>> data['LABEL'] = otp.ops.map_range(data['HOUR'], {'pre-open': (4, 9), 'market': (9, 16)})
>>> otp.run(data)
                     Time  HOUR     LABEL
0 2003-12-01 00:00:00.000     0
1 2003-12-01 00:00:00.001     3
2 2003-12-01 00:00:00.002     6  pre-open
3 2003-12-01 00:00:00.003     9    market
4 2003-12-01 00:00:00.004    12    market
5 2003-12-01 00:00:00.005    15    market
6 2003-12-01 00:00:00.006    18
7 2003-12-01 00:00:00.007    21
8 2003-12-01 00:00:00.008    24
```

Setting `default` value:

```
>>> data = otp.Ticks(HOUR=list(range(0, 25, 3)))
>>> data['LABEL'] = otp.ops.map_range(data['HOUR'], {'pre-open': (4, 9), 'market': (9, 16)}, default='closed')
>>> otp.run(data)
                     Time  HOUR     LABEL
0 2003-12-01 00:00:00.000     0    closed
1 2003-12-01 00:00:00.001     3    closed
2 2003-12-01 00:00:00.002     6  pre-open
3 2003-12-01 00:00:00.003     9    market
4 2003-12-01 00:00:00.004    12    market
5 2003-12-01 00:00:00.005    15    market
6 2003-12-01 00:00:00.006    18    closed
7 2003-12-01 00:00:00.007    21    closed
8 2003-12-01 00:00:00.008    24    closed
```

##### SEE ALSO
**MAP_RANGE** OneTick function

