# otp.Config

### ``class Config(config=None, locator=None, acl=None, otq_path=None, csv_path=None, clean_up=utils.default, copy=True, session_ref=None, license=None, variables=None)``

Bases: `_FileHandler`

The object to create and modify OneTick main configuration file.

This object can be used when creating ``otp.Session`` object.

* **Parameters:**
  * **config** (*str* *or* *Config*) – 

    Allows to specify a custom config.

    Default is None, which means to generate configuration file automatically.
    It will include some default OneTick variables set.
  * **locator** (``otp.Locator``                  or dict`str, [`otp.Locator``]                  or ``otp.RemoteTS``) – 

    Allows to specify a custom locator file.

    If **dict** passed, adds locators passed as values to corresponding contexts from keys.
    For default context pass locator by **DEFAULT** dictionary key.

    If ``otp.RemoteTS``
    then locator file pointing to the remote server will be created.

    Default is None, which means to generate locator file automatically.
    It will include some default databases like COMMON
    and ``otp.config.default_db``.
  * **acl** (``otp.ACL``) – 

    Allows to specify a custom ACL file.

    Default is None, which means to generate ACL file automatically.
    It will include current user with permissions to execute EPs and read/write databases.
  * **otq_path** (*list* *of* *paths to lookup queries*) – OTQ_PATH parameter in the OneTick config file. Default is None, that is equal to the empty list.
  * **csv_path** (*list* *of* *paths to lookup csv files*) – CSV_PATH parameter in the OneTick config file. Default is None, that is equal to the empty list.
  * **clean_up** (*bool*) – 

    If True, then temporary config file will be removed when the Config instance will be destroyed.
    It is helpful for debug purpose.

    By default,
    ``otp.config.clean_up_tmp_files`` is used.
  * **copy** (*bool*) – If True, then the passed custom config file will be copied firstly before any usage with it.
    It might be used when you want to work with a custom config file, but don’t want to change to
    change the original file; in that case a custom config will be copied into a temporary config
    file and every request for modification will be executed for that temporary config. Default
    is True.
  * **license** (*instance from the onetick.py.license module*) – License to use. If it is not set, then onetick.py.license.Default is used.
  * **variables** (*dict*) – Other values to pass to config.

##### Examples

Configuration object can be created with existing path:

```
>>> config = otp.Config('/path/to/the/config')
```

Or it can be created automatically with some default values:

```
>>> config = otp.Config()
>>> config.path
'/tmp/test_username/run_20260722_145505_4775/carrot-unicorn.cfg'
```

Custom locator and ACL files can be specified:

```
>>> config = otp.Config(
...     locator=otp.Locator(...),
...     acl=otp.ACL(...)
... )
```

``otp.RemoteTS`` object can also be specified as `locator`:

```
>>> config = otp.Config(
...     locator=otp.RemoteTS('path.to.the.server.com:50015'),
... )
```

##### SEE ALSO
``otp.Session``
``otp.Locator``
``otp.ACL``
