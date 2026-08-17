# otp.Locator

### ``class Locator(path=None, clean_up=utils.default, copy=True, empty=False, session_ref=None)``

Bases: `_FileHandler`

Class representing OneTick database locator.
Locator is the file that describes database name, location and other options.

This object can be used when creating ``otp.Config`` object.

* **Parameters:**
  * **path** (*str*) – 

    A path to custom locator file.

    Default is None, which means to generate locator file automatically.
  * **clean_up** (*bool*) – 

    If True, then temporary locator will be removed when Locator object will be destroyed. It is
    helpful for debug purpose.

    By default,
    ``otp.config.clean_up_tmp_files`` is used.
  * **copy** (*bool*) – If True, then the passed custom locator by the `path` parameter will be copied firstly before
    usage. It might be used when you want to work with a custom locator, but don’t want to change
    the original file; in that case a custom locator will be copied into a temporary locator and
    every request for modification will be executed for that temporary locator. Default is True.
  * **empty** (*bool*) – 

    If True, then a temporary locator will have no databases.

    Default is False, which means it will include some default databases like COMMON
    and ``otp.config.default_db``.

##### Examples

Locator object can be created with existing path:

```
>>> locator = otp.Locator('/path/to/the/locator')
```

Or it can be created automatically with some default values:

```
>>> locator = otp.Locator()
>>> locator.path
'/tmp/test_username/run_20260722_145505_4775/observant-jackrabbit.locator'
```

##### SEE ALSO
``otp.Session``
``otp.Config``
``otp.ACL``
