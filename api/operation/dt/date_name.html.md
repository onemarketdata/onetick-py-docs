# otp.Operation.dt.date_name

#### \_DtAccessor.date_name(date_part, timezone)

Returns a number representing the specified `date_part` of the specified datetime,
interpreted in the specified `timezone`.

* **Parameters:**
  * **date_part** (*str* *|* *Operation* *|* *Column*) – 

    Possible values are:
    : `year`, `quarter`, `month`,
      `week`, `weekday`, `day`, `dayofyear`,
      `hour`, `minute`, `second`,
      `millisecond`, `nanosecond`.
  * **timezone** (*str* *|* *Operation* *|* *Column*) – Name of the timezone, an operation or a column with it.
    By default, the timezone of the query will be used.

##### Examples

```
>>> data = otp.Ticks(X=[otp.dt(2020, 11, 11, 5, 4, 13, 101737, 879)] * 12,
...                  DATE_PART=['year', 'quarter', 'month',
...                             'week', 'weekday', 'day', 'dayofyear',
...                             'hour', 'minute', 'second',
...                             'millisecond', 'nanosecond'])
>>> data['DATE_NAME'] = data['X'].dt.date_name(data['DATE_PART'])
>>> otp.run(data)[['X', 'DATE_NAME', 'DATE_PART']]
                               X  DATE_NAME    DATE_PART
0  2020-11-11 05:04:13.101737879       2020         year
1  2020-11-11 05:04:13.101737879          4      quarter
2  2020-11-11 05:04:13.101737879         11        month
3  2020-11-11 05:04:13.101737879         46         week
4  2020-11-11 05:04:13.101737879          3      weekday
5  2020-11-11 05:04:13.101737879         11          day
6  2020-11-11 05:04:13.101737879        315    dayofyear
7  2020-11-11 05:04:13.101737879          5         hour
8  2020-11-11 05:04:13.101737879          4       minute
9  2020-11-11 05:04:13.101737879         13       second
10 2020-11-11 05:04:13.101737879        101  millisecond
11 2020-11-11 05:04:13.101737879  101737879   nanosecond
```

##### SEE ALSO
**DATENAME** OneTick function

