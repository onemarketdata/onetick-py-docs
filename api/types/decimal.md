# otp.decimal

### ``class decimal(*args, **kwargs)``

Bases: ``object``

Object that represents decimal OneTick value.
Decimal is 128 bit base 10 floating point number.

* **Parameters:**
  **value** (*int* *,* *float* *,* *str*) – The value to initialize decimal from.
  Note that float values may be converted with precision lost.

##### Examples

``decimal`` objects can be used in tick generators
and column operations as any other onetick-py type:

```
>>> t = otp.Ticks({'A': [otp.decimal(1), otp.decimal(2)]})
>>> t['B'] = otp.decimal(1.23456789)
>>> t['C'] = t['A'] / 0
>>> t['D'] = t['A'] + otp.nan
>>> otp.run(t)
                     Time    A         B    C    D
0 2003-12-01 00:00:00.000  1.0  1.234568  inf  NaN
1 2003-12-01 00:00:00.001  2.0  1.234568  inf  NaN
```

Additionally, any arithmetic operation with ``decimal`` object will return
an ``Operation`` object:

```
>>> t = otp.Tick(A=1)
>>> t['X'] = otp.decimal(1) / 0
>>> otp.run(t)
        Time    A    X
0 2003-12-01    1  inf
```

Note that converting from float (first row) may result in losing precision.
``decimal`` objects are created from strings or integers, so they don’t lose precision:

```
>>> t0 = otp.Tick(A=0.1)
>>> t1 = otp.Tick(A=otp.decimal(0.01))
>>> t2 = otp.Tick(A=otp.decimal('0.001'))
>>> t3 = otp.Tick(A=otp.decimal(1) / otp.decimal(10_000))
>>> t = otp.merge([t0, t1, t2, t3], enforce_order=True)
>>> t['STR_A'] = t['A'].decimal.str(34)
>>> otp.run(t)
        Time       A                                 STR_A
