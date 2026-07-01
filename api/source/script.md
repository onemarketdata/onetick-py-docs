# otp.Source.script

#### ``Source.script(func, inplace=False)``

Implements a script for every tick.

Allows to pass a `func` that will be applied per every tick.
A `func` can be python callable in this case it will be translated to per tick script.
In order to use it in Remote OTP with Ray, the function should be decorated with `@otp.remote`,
see `Ray usage examples` for details.

See `Per Tick Script Guide` for more detailed description
of python to OneTick code translation and per-tick script features.

The script written in per tick script language can be passed itself as a string or path to a file with the code.
onetick-py doesn’t validate the script, but configure the schema accordingly.

* **Parameters:**
  * **func** (*callable* *,* *str* *or* *path*) – 
    - a callable that takes only one parameter - actual tick that behaves like a Source instance
    - or the script on per-tick script language
    - or a path to file with onetick script
  * **self** (*Source*)
* **Return type:**
  ``Source``

