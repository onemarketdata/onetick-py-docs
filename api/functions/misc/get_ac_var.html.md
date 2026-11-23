# otp.ops.get_ac_var

### ``get_ac_var(name)``

Returns the value of the specified access control variable for the current user.

If the variable is not set, an empty string is returned.

* **Parameters:**
  **name** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(
...     SERVER_LOCATION=otp.ops.get_ac_var('SERVER_LOCATION'),
... )
>>> otp.run(data)
        Time  SERVER_LOCATION
0 2003-12-01   localhost:4003
```

##### SEE ALSO
**GET_AC_VAR** OneTick function

