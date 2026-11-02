# otp.today

### ``today(timezone=None)``

Returns the current date in the specified `timezone`.

* **Parameters:**
  **timezone** (str | ``Operation``) – 

  The timezone name to use.
  Special value `local` can be used to use local timezone name.

  By default the timezone of the query is used.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['TODAY'] = otp.today()
>>> otp.run(data)
        Time  A       TODAY
0 2003-12-01  1  2026-09-25
```

##### SEE ALSO
**TODAY** OneTick function

**CURRENT_DATE**/**CURDATE** OneTick function

