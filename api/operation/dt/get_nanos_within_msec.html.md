# otp.Operation.dt.get_nanos_within_msec

#### \_DtAccessor.get_nanos_within_msec()

Returns number of nanoseconds retained in a millisecond from a timestamp value.

##### Examples

```
>>> data = otp.Ticks(X=[otp.dt(2022, 5, 1, 15, 0, 6, 123, i) for i in range(10, 17)])
>>> data['Y'] = data['X'].dt.get_nanos_within_msec()
>>> otp.run(data)[['X', 'Y']]
                              X       Y
0 2022-05-01 15:00:06.000123010  123010
1 2022-05-01 15:00:06.000123011  123011
2 2022-05-01 15:00:06.000123012  123012
3 2022-05-01 15:00:06.000123013  123013
4 2022-05-01 15:00:06.000123014  123014
5 2022-05-01 15:00:06.000123015  123015
6 2022-05-01 15:00:06.000123016  123016
```

##### SEE ALSO
**GET_NANOS_WITHIN_MSEC** OneTick function

