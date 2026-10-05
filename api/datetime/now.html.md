# otp.now

### ``now(precision=None)``

Returns the current datetime in the timezone of the query.

* **Parameters:**
  **precision** (int or ``Operation``) – Determines the milliseconds precision of the returned timestamp value.
  Valid values are 0-3.
  Default value is 3.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['NOW'] = otp.now()
>>> otp.run(data)
        Time  A                      NOW
0 2003-12-01  1  2025-09-29 09:09:00.158
```

##### SEE ALSO
**NOW** OneTick function

**CURRENT_TIME**/**CURRENT_TIMESTAMP** OneTick function

