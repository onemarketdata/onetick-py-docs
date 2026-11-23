# otp.ops.get_environment_var

### ``get_environment_var(name)``

Returns the value of the environment variable
from client (when symbol is `LOCAL::`) or from server (when symbol is a database configured on server side).

Returns empty string if such variable is absent.

* **Parameters:**
  **name** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(
...     SHELL=otp.ops.get_environment_var('SHELL'),
...     PATH=otp.ops.get_environment_var('PATH').astype(otp.string[100]),
...     PWD=otp.ops.get_environment_var('PWD'),
... )
>>> otp.run(data)
        Time      SHELL                                          PATH                    PWD
0 2003-12-01  /bin/bash  /home/user/onetick-py/.venv/bin:/home/use...  /home/user/onetick-py
```

##### SEE ALSO
**GET_ENVIRONMENT_VAR** OneTick function

