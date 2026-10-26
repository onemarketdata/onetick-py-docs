# otp.Source.hide_ticks_with_status

#### ``Source.hide_ticks_with_status(inplace=False)``

Makes visible ticks with **TICK_STATUS** not equal to 0 or 8 (which stands for INSERT) invisible,
so they are treated the same way all invisible ticks are treated.

This method has effect that is opposite to the effect of ``show_hidden_ticks()``.
It can be used to construct or fix order books, as well as to inject or modify correction/cancellation ticks.

* **Parameters:**
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise, method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Hidden ticks with non-zero **TICK_STATUS** can be seen with ``show_hidden_ticks()``:

```
>>> data = otp.DataSource(db='CME_SAMPLE', tick_type='PRL_FULL', symbols=r'NQ\H24')
>>> data = data.show_hidden_ticks()
>>> data = data[['UPDATE_TYPE', 'PRICE', 'SIZE', 'RECORD_TYPE', 'TICK_STATUS']]
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                            Time UPDATE_TYPE     PRICE  SIZE RECORD_TYPE  TICK_STATUS
0  2024-02-01 00:00:00.211493687                   NaN     0           B           32
1  2024-02-01 00:00:00.211493687           A  17317.75     1           R            0
2  2024-02-01 00:00:00.211493687                   NaN     0           E           33
3  2024-02-01 00:00:00.211541475                   NaN     0           B           32
4  2024-02-01 00:00:00.211541475           D  17317.00     0           R            0
...
```

Use this method to make them invisible again:

```
>>> data = otp.DataSource(db='CME_SAMPLE', tick_type='PRL_FULL', symbols=r'NQ\H24')
>>> data = data.show_hidden_ticks()
>>> data = data.hide_ticks_with_status()
>>> data = data[['UPDATE_TYPE', 'PRICE', 'SIZE', 'RECORD_TYPE', 'TICK_STATUS']]
>>> data = data.limit(100)
>>> otp.run(data, date=otp.dt(2024, 2, 1))
                            Time UPDATE_TYPE     PRICE  SIZE RECORD_TYPE  TICK_STATUS
0  2024-02-01 00:00:00.211493687           A  17317.75     1           R            0
1  2024-02-01 00:00:00.211541475           D  17317.00     0           R            0
2  2024-02-01 00:00:00.211630059           A  17317.25     1           R            0
3  2024-02-01 00:00:00.211642827           A  17317.75     1           R            0
4  2024-02-01 00:00:00.211654537           D  17317.25     0           R            0
...
```

##### SEE ALSO
**HIDE_TICKS_WITH_STATUS** OneTick event processor

``show_hidden_ticks()``

