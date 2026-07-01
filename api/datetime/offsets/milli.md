# otp.Milli

### ``Milli(n)``

Object representing millisecond’s datetime offset.

Can be added to or subtracted from:

* ``otp.datetime`` objects
* ``Source`` columns of datetime type

* **Parameters:**
  **n** (int, ``Column``, ``Operation``, float) – Offset integer value or column of ``Source``.
  The only ``Operation`` supported is
  subtracting one datetime column from another. See example below.
  Offset could be `float` to pass a fractional time unit value.

##### Examples

Add to or subtract from ``otp.datetime`` object:

```
>>> otp.datetime(2012, 12, 12, 12) + otp.Milli(1)
2012-12-12 12:00:00.001000
>>> otp.datetime(2012, 12, 12, 12) - otp.Milli(1)
2012-12-12 11:59:59.999000
```

Using `float` value to pass nanoseconds:

```
>>> otp.datetime(2012, 12, 12, 12) + otp.Milli(1.000123)
2012-12-12 12:00:00.001000123
```
