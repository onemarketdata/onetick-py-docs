# otp.Column.time_shift

#### ``Column.time_shift(shift_time, , , selection_criteria=None, timestamp_field='TIMESTAMP', group_by=None)``

Returns the value of the specified field, from a tick,
whose timestamp differs from current tick’s timestamp by `shift_time`.

If `shift_time` is negative, it returns the value for the preceding tick,
and if `shift_time` is positive, succeeding ticks (those that have not arrived yet) are considered.

For shifts crossing the boundaries of query time range default values by type will be returned:
0 for numbers, empty strings for strings etc.

* **Parameters:**
  * **shift_time** (*int* *or* *float*) – 

    Integer values are treated as milliseconds
    and float values are treated as `milliseconds[.nanoseconds]` format.

    #### NOTE
    Positive shift times are allowed only when adding fields and in per-tick script.
  * **selection_criteria** (*str*) – 

    Possible values for the criteria parameter are:
    * *last_before*
    * *last_at_or_before* (default for negative shift times)
    * *first_after*
    * *first_at_or_after* (default for positive shift times)
  * **timestamp_field** (*str*) – 

    Specifies an alternative timestamp field name
    (values in this field are assumed to be in non-decreasing order).

    By default the tick’s TIMESTAMP field is used.
  * **group_by** (*str* *|* *list* **[*str* *]*) – 

    Specifies a field name or a list of field names,
    in which case selection is performed among the ticks with same values of the specified fields.

    #### NOTE
    This parameter can be set only with negative time shifts.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=[1, 2, 3, 4, 5, 6, 7, 8, 9], B=[1, 1, 1, 2, 2, 3, 3, 2, 3])
>>> data['A1_AT'] = data['A'].time_shift(1, selection_criteria='first_at_or_after')
>>> data['A1_AFTER'] = data['A'].time_shift(1, selection_criteria='first_after')
>>> data['AM1_AT_GROUP_BY_B'] = data['A'].time_shift(-1, group_by='B', timestamp_field='TIMESTAMP')
>>> otp.run(data)
                     Time  A  B  A1_AT  A1_AFTER  AM1_AT_GROUP_BY_B
0 2003-12-01 00:00:00.000  1  1      2         3                  0
1 2003-12-01 00:00:00.001  2  1      3         4                  1
2 2003-12-01 00:00:00.002  3  1      4         5                  2
3 2003-12-01 00:00:00.003  4  2      5         6                  0
4 2003-12-01 00:00:00.004  5  2      6         7                  4
5 2003-12-01 00:00:00.005  6  3      7         8                  0
6 2003-12-01 00:00:00.006  7  3      8         9                  6
7 2003-12-01 00:00:00.007  8  2      9         0                  5
8 2003-12-01 00:00:00.008  9  3      0         0                  7
```

##### SEE ALSO
``tick_shift()``

**TIME_SHIFT** OneTick function

