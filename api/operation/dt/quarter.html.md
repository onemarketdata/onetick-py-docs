# otp.Operation.dt.quarter

#### \_DtAccessor.quarter(timezone)

Return the quarter number.

* **Parameters:**
  **timezone** (*str* *|* *Operation* *|* *Column*) – Name of the timezone, an operation or a column with it.
  By default, the timezone of the query will be used.

##### Examples

```
>>> data = otp.Ticks(X=[otp.dt(2022, i, 1) for i in range(1, 13)])
>>> data['QUARTER'] = data['X'].dt.quarter()
>>> otp.run(data)[['X', 'QUARTER']]
            X  QUARTER
0  2022-01-01        1
1  2022-02-01        1
2  2022-03-01        1
3  2022-04-01        2
4  2022-05-01        2
5  2022-06-01        2
6  2022-07-01        3
7  2022-08-01        3
8  2022-09-01        3
9  2022-10-01        4
10 2022-11-01        4
11 2022-12-01        4
```
