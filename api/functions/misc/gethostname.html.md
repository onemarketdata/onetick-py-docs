# otp.ops.gethostname

### ``gethostname()``

Returns the name of the host where this function runs.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(HOST_NAME=otp.ops.gethostname())
>>> otp.run(data)
        Time        HOST_NAME
0 2003-12-01  DESKTOP-EUI4SLI
```

##### SEE ALSO
**GETHOSTNAME** OneTick function

