# otp.Operation.dt.month

#### \_DtAccessor.month(timezone)

Return the month number.

* **Parameters:**
  **timezone** (*str* *|* *Operation* *|* *Column*) – Name of the timezone, an operation or a column with it.
  By default, the timezone of the query will be used.

##### Examples

```
>>> data = otp.Ticks(X=[otp.dt(2022, i, 1) for i in range(1, 13)])
>>> data['MONTH'] = data['X'].dt.month()
>>> otp.run(data)[['X', 'MONTH']]
            X  MONTH
0  2022-01-01      1
1  2022-02-01      2
2  2022-03-01      3
3  2022-04-01      4
4  2022-05-01      5
5  2022-06-01      6
6  2022-07-01      7
7  2022-08-01      8
8  2022-09-01      9
9  2022-10-01     10
10 2022-11-01     11
11 2022-12-01     12
```
