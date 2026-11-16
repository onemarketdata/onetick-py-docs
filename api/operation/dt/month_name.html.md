# otp.Operation.dt.month_name

#### \_DtAccessor.month_name(timezone)

Return the name of the month.

* **Parameters:**
  **timezone** (*str* *|* *Operation* *|* *Column*) – Name of the timezone, an operation or a column with it.
  By default, the timezone of the query will be used.

##### Examples

```
>>> data = otp.Ticks(X=[otp.dt(2022, i, 1) for i in range(1, 13)])
>>> data['MONTH_NAME'] = data['X'].dt.month_name()
>>> otp.run(data)[['X', 'MONTH_NAME']]
            X MONTH_NAME
0  2022-01-01        Jan
1  2022-02-01        Feb
2  2022-03-01        Mar
3  2022-04-01        Apr
4  2022-05-01        May
5  2022-06-01        Jun
6  2022-07-01        Jul
7  2022-08-01        Aug
8  2022-09-01        Sep
9  2022-10-01        Oct
10 2022-11-01        Nov
11 2022-12-01        Dec
```
