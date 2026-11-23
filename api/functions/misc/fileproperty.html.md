# otp.ops.fileproperty

### ``fileproperty(path, property)``

Returns the specified `property` value from file `path`.

If specified `path` was not found function will return -1.

* **Parameters:**
  * **path** (str, ``Operation``)
  * **property** (str, ``Operation``) – Supported values for `property` are `IS_READ_ONLY` and `BYTES_USED` (number of bytes used by the file).
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=['/dev/null', '/etc/group', '/a/b/c/d/e/f'])
>>> data['IS_READ_ONLY'] = otp.ops.fileproperty(data['A'], 'IS_READ_ONLY')
>>> data['BYTES_USED'] = otp.ops.fileproperty(data['A'], 'BYTES_USED')
>>> otp.run(data)
                     Time             A  IS_READ_ONLY  BYTES_USED
0 2003-12-01 00:00:00.000     /dev/null             0           0
1 2003-12-01 00:00:00.001    /etc/group             1         810
2 2003-12-01 00:00:00.002  /a/b/c/d/e/f            -1          -1
```

##### SEE ALSO
**FILEPROPERTY** OneTick function

