# otp.ops.basename

### ``basename(path)``

Returns file name from the given `path`.

* **Parameters:**
  **path** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=['/dev/null', '/etc/group', '/a/b/c/d/e/f'])
>>> data['NAME'] = otp.ops.basename(data['A'])
>>> otp.run(data)
                     Time             A   NAME
0 2003-12-01 00:00:00.000     /dev/null   null
1 2003-12-01 00:00:00.001    /etc/group  group
2 2003-12-01 00:00:00.002  /a/b/c/d/e/f      f
```

##### SEE ALSO
**BASENAME** OneTick function

