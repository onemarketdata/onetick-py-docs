# otp.Operation.str.slice

### ``slice(start=None, stop=None)``

Returns slice.

* **Parameters:**
  * **start** (*int* *or* *Column* *or* *Operation* *,* *optional*) – Start position for slice operation.
  * **stop** (*int* *or* *Column* *or* *Operation* *,* *optional*) – Stop position for slice operation.

##### Examples

```
>>> data = otp.Ticks(X=['12345', 'abcde', 'qwerty'], START=[3, 0, 1], STOP=[4, 3, 3])
>>> data['START_1_SLICE'] = data['X'].str.slice(start=1)
>>> data['STOP_2_SLICE'] = data['X'].str.slice(stop=2)
>>> data['SLICE_FROM_COLUMNS'] = data['X'].str.slice(start=data['START'], stop=data['STOP'])
>>> otp.run(data)
                             Time       X  START  STOP START_1_SLICE STOP_2_SLICE SLICE_FROM_COLUMNS
0 2003-12-01 00:00:00.000   12345      3     4          2345           12                  4
1 2003-12-01 00:00:00.001   abcde      0     3          bcde           ab                abc
2 2003-12-01 00:00:00.002  qwerty      1     3         werty           qw                 we
```

Parameters can be negative:

```
>>> data = otp.Ticks(X=['12345', 'abcde', 'qwerty'])
>>> data['START_SLICE'] = data['X'].str.slice(start=-3)
>>> data['STOP_SLICE'] = data['X'].str.slice(stop=-1)
