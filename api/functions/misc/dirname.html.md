# otp.ops.dirname

### ``dirname(path)``

Returns the path to the parent directory of the given `path`.

* **Parameters:**
  **path** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=['/dev/null', '/etc/group', '/a/b/c/d/e/f'])
>>> data['DIR'] = otp.ops.dirname(data['A'])
>>> otp.run(data)
                     Time             A          DIR
0 2003-12-01 00:00:00.000     /dev/null        /dev/
1 2003-12-01 00:00:00.001    /etc/group        /etc/
2 2003-12-01 00:00:00.002  /a/b/c/d/e/f  /a/b/c/d/e/
```

##### SEE ALSO
**DIRNAME** OneTick function

