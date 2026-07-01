# otp.Week

### ``Week(n)``

Object representing week’s datetime offset.

Can be added to or subtracted from:

* ``otp.datetime`` objects
* ``Source`` columns of datetime type

* **Parameters:**
  **n** (int, ``Column``, ``Operation``) – Offset integer value or column of ``Source``.
  The only ``Operation`` supported is
  subtracting one datetime column from another. See example below.

##### Examples

Add to or subtract from ``otp.datetime`` object:

```
>>> otp.datetime(2012, 12, 12, 12) + otp.Week(1)
2012-12-19 12:00:00
>>> otp.datetime(2012, 12, 12, 12) - otp.Week(1)
2012-12-05 12:00:00
```
