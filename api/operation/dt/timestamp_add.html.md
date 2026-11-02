# otp.Operation.dt.timestamp_add

#### \_DtAccessor.timestamp_add(date_part, number)

Returns the specified datetime with the specified `number` interval (signed integer)
added to the specified `date_part` of that datetime.

* **Parameters:**
  * **number** (*int* *|* *Operation* *|* *Column*) – Number of intervals to add.
  * **date_part** (*str* *|* *Operation* *|* *Column*) – 

    Supported values are:
    : ’SQL_TSI_YEAR’, ‘SQL_TSI_QUARTER’, ‘SQL_TSI_MONTH’, ‘SQL_TSI_WEEK’,
      ‘SQL_TSI_DAY’, ‘SQL_TSI_HOUR’, ‘SQL_TSI_MINUTE’, ‘SQL_TSI_SECOND’.

##### Examples

Add one interval:

```
>>> data = otp.Ticks(
...     X=[otp.dt(2020, 11, 12)] * 5,
...     DATE_PART=['SQL_TSI_YEAR', 'SQL_TSI_QUARTER', 'SQL_TSI_MONTH', 'SQL_TSI_WEEK', 'SQL_TSI_DAY']
... )
>>> data['Y'] = data['X'].dt.timestamp_add(data['DATE_PART'], 1)
>>> otp.run(data)[['X', 'DATE_PART', 'Y']]
           X        DATE_PART           Y
0 2020-11-12     SQL_TSI_YEAR  2021-11-12
1 2020-11-12  SQL_TSI_QUARTER  2021-02-10
2 2020-11-12    SQL_TSI_MONTH  2020-12-12
3 2020-11-12     SQL_TSI_WEEK  2020-11-19
4 2020-11-12      SQL_TSI_DAY  2020-11-13
```

Subtract one interval:

```
>>> data = otp.Ticks(X=[otp.dt(2020, 11, 11, 5, 4, 13)] * 3,
...                  DATE_PART=['SQL_TSI_HOUR', 'SQL_TSI_MINUTE', 'SQL_TSI_SECOND'])
>>> data['Y'] = data['X'].dt.timestamp_add(data['DATE_PART'], -1)
>>> otp.run(data)[['X', 'DATE_PART', 'Y']]
                    X       DATE_PART                    Y
0 2020-11-11 05:04:13    SQL_TSI_HOUR  2020-11-11 04:04:13
1 2020-11-11 05:04:13  SQL_TSI_MINUTE  2020-11-11 05:03:13
2 2020-11-11 05:04:13  SQL_TSI_SECOND  2020-11-11 05:04:12
```

##### SEE ALSO
**TIMESTAMPADD** OneTick function

