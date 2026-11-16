# otp.Operation.dt.as_yyyymmddhhmmss

#### \_DtAccessor.as_yyyymmddhhmmss(timezone)

Converts the timestamp into the integer in the form YYYYMMDDhhmmss.

* **Parameters:**
  **timezone** (*str* *|* *Operation* *|* *Column*) – Name of the timezone, an operation or a column with it.
  By default, the timezone of the query will be used.

##### Examples

```
>>> data = otp.Ticks(X=[otp.dt(2020, i, i, i, i, i, i) for i in range(1, 5)])
>>> data['Y'] = data['X'].dt.as_yyyymmddhhmmss()
>>> otp.run(data)[['X', 'Y']]
                           X               Y
0 2020-01-01 01:01:01.000001  20200101010101
1 2020-02-02 02:02:02.000002  20200202020202
2 2020-03-03 03:03:03.000003  20200303030303
3 2020-04-04 04:04:04.000004  20200404040404
```

##### SEE ALSO
**AS_YYYYMMDDHHMMSS** OneTick function

