

# otp.Session: set up OneTick configuration files

`onetick-py` provides tools for managing OneTick configuration files and databases
required to run OneTick locally (without WebAPI).

#### NOTE
In WebAPI mode creating OneTick configuration files is not needed, because it’s managed by WebAPI OneTick server.

## Existing OneTick configuration

OneTick uses **ONE_TICK_CONFIG** environment variable to get the path to the configuration file.

If this variable is already set, then `onetick-py` can be used right away,
even without creating ``otp.Session`` object:

```
>>> import os
>>> from pathlib import Path
>>> os.environ['ONE_TICK_CONFIG'] = 'one_tick_config.txt'
>>> Path('one_tick_config.txt').write_text('DB_LOCATOR.DEFAULT=one_tick_locator.txt')
>>> Path('one_tick_locator.txt').write_text('<VERSION_INFO VERSION="2"/><DATABASES></DATABASES>')

>>> import onetick.py as otp
>>> t = otp.Tick(A=1)
>>> otp.run(t, symbols='LOCAL::', date=otp.dt(2022, 1, 1))
        Time  A
0 2022-01-01  1
```

## Creating session

Session can be created with ``otp.Session`` class:

```
>>> import onetick.py as otp
>>> session = otp.Session()
>>> # make required queries
>>> t = otp.Tick(A=1)
>>> otp.run(t, symbols='LOCAL::', date=otp.dt(2022, 1, 1))
        Time  A
0 2022-01-01  1
>>> session.close()
```

To avoid manually closing session, you can create it as a python context manager:

```
>>> import onetick.py as otp
>>> with otp.Session() as session:
...     # make required queries
...     t = otp.Tick(A=1)
...     df = otp.run(t, symbols='LOCAL::', date=otp.dt(2022, 1, 1))
...     print(df)
        Time  A
0 2022-01-01  1
```

## Setting up custom OneTick configuration

If you want override default temporary config, you can either pass path to config file or
``otp.Config`` object as ``otp.Session`` `config`
constructor parameter.

```
config = otp.Config('/path/to/config')
session = otp.Session(config)
```

## Setting up custom database locator

If you want to create default configuration files, but override the locator file,
you can use ``otp.Locator`` object:

```
config=otp.Config(
    locator=otp.Locator('/path/to/locator')
)
session = otp.Session(config)
```

The object ``otp.RemoteTS`` can also be used
to automatically create locator file pointing to the remote server:

```
config=otp.Config(
    locator=otp.RemoteTS('path.to.the.server.com:50015')
)
session = otp.Session(config)
```

## Setting up custom ACL

By default, a temporary generated ``otp.ACL`` object is created for every
``otp.Config`` and respectively for each session.

However you could pass path to ACL configuration file if you need to load custom ACL.

```
acl = otp.ACL('/path/to/acl')
config = otp.Config(acl=acl)
session = otp.Session(config)
```

You can also add entities to the ACL by using ``otp.ACL.add`` method or
remove entities using ``otp.ACL.remove``.

```
session.acl.add(otp.ACL.User('new_user'))
session.acl.remove(otp.ACL.User('old_user'))
```

## Creating temporary database

To create and add a temporary database to the locator, just create an ``otp.DB`` object and
pass it to the ``otp.Session.use`` method.

```
>>> db = otp.DB('DB_NAME')
>>> session.use(db)
```

To add data to temporary database use ``otp.DB.add`` method:

```
>>> db.add(otp.Ticks(A=[1, 2, 3]), date=otp.dt(2003, 1, 1), symbol='SYM', tick_type='TT')
```

Alternatively, if you already have the data you want to add to the database, you could pass
``otp.Source`` object as ``otp.DB`` constructor second parameter:

```
>>> data = otp.Ticks(A=[1, 2, 3])
>>> db = otp.DB('DB_NAME', data)
>>> session.use(db)
```

## Working with existing databases

Adding an existing database to the locator almost the same, as for temporary database.
However, you need to specify locations to load database from via `db_locations` parameter.

```
>>> db = otp.DB('NEW_DB', db_locations=[{'location': '/home/user/data/NEW_DB'}])
>>> session.use(db)
```

Additional locator configuration variables could be set via `db_locations` and `db_properties` parameters,
for `location` and `db` sections of database description in a locator configuration file correspondingly.

```
>>> db = otp.DB(
...     'TEST_DB',
...     db_properties={
...         'symbology': 'SYM',
...         'tick_timestamp_type': 'NANOS',
...     },
...     db_locations=[{
...         'access_method': otp.core.db_constants.access_method.FILE,
...         'location': '/path/to/test_db/',
...         'start_time': datetime(year=2003, month=1, day=1),
...         'end_time': datetime(year=2023, month=1, day=1),
...     }],
... )
```

See `OneTick Locator Variables` OneTick documentation for available locator configuration variables.

## Remote databases

Remote servers can be added to OneTick database locator too
by passing ``otp.RemoteTS`` object
to the ``otp.Session.use`` method:

```
session.use(otp.RemoteTS('path.to.the.server.com:50015'))
```

Or they can be added when creating ``otp.Session``:

```
>>> import onetick.py as otp
>>> with otp.Session(
...     config=otp.Config(
...         locator=otp.RemoteTS('path.to.the.server.com:50015')
...     )
... ):
...     # get available databases
...     print(otp.databases(as_table=True)['DB_NAME'])
0                ABAXX
1          ABAXX_DAILY
2            ABU_DHABI
3       ABU_DHABI_BARS
4      ABU_DHABI_DAILY
            ...
793        XETRA_DAILY
794          ZHENGZHOU
795     ZHENGZHOU_BARS
796    ZHENGZHOU_DAILY
797            __OQD__
```

## Derived databases

Derived databases could be added to the locator like a regular database.
Of course, a parent database must be added to create a derived database.

```
>>> db = otp.DB('DB_NAME')
>>> session.use(db)
>>> derived_db = otp.DB('DB_NAME//DERIVED_LABEL')
>>> session.use(derived_db)
```

You can also add data to derived database.

```
>>> data = otp.Ticks(A=[1, 2, 3])
>>> derived_db = otp.DB('DB_NAME//DERIVED_LABEL')
>>> session.use(derived_db)
>>> derived_db.add(data)
```

See `Derived Databases` OneTick documentation for more info about derived databases.

## Useful types of sessions

There are some other types of session classes,
that are inherited from base ``otp.Session`` class,
but provide some additional functionality.

### otp.TestSession

``otp.TestSession`` sets up some default onetick.py configuration values
and is useful for the purposes of quickly setting up environment to test some simple queries.

### onetick.hosted.Session

`onetick.hosted.Session` automatically scans directory structure on the local machine
finding all OneTick databases, and creating OneTick locator that allows to access them
without the need of additional configuration.

`onetick.hosted` is a separate module located in the
`onetick-hosted` project
on our Gitlab server.
You can find all usage instructions and some examples in the
`README.md` file.

`onetick.hosted` can be installed with `pip`:

```
pip install onetick-hosted
```

## Creating session with different contexts



In OneTick context is a namespace for the databases.

Different contexts allow having sets of databases from different places, local or remote,
and easily switching context with parameter `context` supported by many onetick-py functions.

Default context is named **DEFAULT** and is created automatically by ``otp.Session``.
You can see it by reading the configuration file and seeing **DB_LOCATOR.DEFAULT** variable:

```
>>> session = otp.Session()
>>> with open(session.config.path) as r:
...     print(r.read())
ONE_TICK_CONFIG.ALLOW_ENV_VARS=Yes
...
ACCESS_CONTROL_FILE="/tmp/test_onetick/run_20250127_160920_16360/beige-malkoha.acl"
DB_LOCATOR.DEFAULT="/tmp/test_onetick/run_20250127_160920_16360/lurking-frigatebird.locator"
...
```

Default context can be modified with parameter `locator` of ``otp.Config``.
Additional contexts can be created by adding other *DB_LOCATOR.* variables to OneTick configuration file.
Let’s create context **OTHER**, and create databases in both contexts:

```
>>> default_locator = otp.Locator()
>>> default_locator.add(otp.DB('A', otp.Tick(A=1), tick_type='TT', symbol='S'))
>>> other_locator = otp.Locator(empty=True)
>>> other_locator.add(otp.DB('B', otp.Tick(B=2), tick_type='TT', symbol='S'))
>>> config = otp.Config(locator=default_locator,
...                     variables={'DB_LOCATOR.OTHER': other_locator.path})
>>> session = otp.Session(config)
>>> with open(session.config.path) as r:
...     print(r.read())
ONE_TICK_CONFIG.ALLOW_ENV_VARS=Yes
...
ACCESS_CONTROL_FILE="/tmp/test_onetick/run_20250127_160920_16360/ultra-inchworm.acl"
DB_LOCATOR.DEFAULT="/tmp/test_onetick/run_20250127_160920_16360/infrared-crane.locator"
DB_LOCATOR.OTHER="/tmp/test_onetick/run_20250127_160920_16360/tangerine-earthworm.locator"
...
```

After that both contexts can be used when running queries, thus making databases from different locators available:

```
>>> data = otp.DataSource('A', tick_type='TT', symbols='S', schema_policy='manual')
>>> # running query without parameter *context* will run the query in **DEFAULT** context
>>> print(otp.run(data))
        Time  A
0 2003-12-01  1
>>> data = otp.DataSource('B', tick_type='TT', symbols='S', schema_policy='manual')
>>> print(otp.run(data, context='OTHER'))
        Time  B
0 2003-12-01  2
```

Some other functions also have parameter `context`, e.g. ``otp.databases``:

```
>>> otp.databases()
{'A': <onetick.py.db._inspection.DB at 0x7f520daa4160>,
 'COMMON': <onetick.py.db._inspection.DB at 0x7f520daa4280>,
 'DEMO_L1': <onetick.py.db._inspection.DB at 0x7f520daa4400>}
>>> otp.databases(context='OTHER')
{'B': <onetick.py.db._inspection.DB at 0x7f52811c07f0>}
```
