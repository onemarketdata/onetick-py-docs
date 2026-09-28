# otp.Operation.dt.day_of_week

#### \_DtAccessor.day_of_week(start_index, start_day, timezone)

Return the day of the week.

Assuming the week starts on `start_day`, which is denoted by `start_index`.
Default: Monday - 1, …, Sunday - 7; set according to ISO8601

* **Parameters:**
  * **start_index** (*int* *or* *Operation*) – The index of the `start_day`.
  * **start_day** ( *'monday'* *or*  *'sunday'*) – Day that will be denoted with `start_index`
  * **timezone** (*str* *|* *Operation* *|* *Column*) – Name of the timezone, an operation or a column with it.
    By default, the timezone of the query will be used.

##### Examples

```
>>> data = otp.Ticks(X=[otp.dt(2022, 5, i) for i in range(9, 16)])
>>> data['DAY_OF_WEEK'] = data['X'].dt.day_of_week()
>>> otp.run(data)[['X', 'DAY_OF_WEEK']]
           X  DAY_OF_WEEK
0 2022-05-09            1
1 2022-05-10            2
2 2022-05-11            3
3 2022-05-12            4
4 2022-05-13            5
5 2022-05-14            6
6 2022-05-15            7
```
