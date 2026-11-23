# otp.ops.get_os_info

### ``get_os_info(property)``

Returns the value for the specified OS property.

* **Parameters:**
  **property** (str, ``Operation``) – Supported properties are `name`, `version`, `bitness`.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(
...     NAME=otp.ops.get_os_info('name'),
...     VERSION=otp.ops.get_os_info('version'),
...     BITNESS=otp.ops.get_os_info('bitness'),
... )
>>> otp.run(data)
        Time   NAME                            VERSION BITNESS
0 2003-12-01  Linux  6.18.54.1-microsoft-standard-WSL2      64
```

##### SEE ALSO
**GET_OS_INFO** OneTick function

