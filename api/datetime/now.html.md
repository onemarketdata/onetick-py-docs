# otp.now

### ``now()``

Returns the current datetime in the timezone of the query.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data['NOW'] = otp.now()
>>> otp.run(data)
        Time  A                     NOW
0 2003-12-01  1 2025-09-29 09:09:00.158
```
