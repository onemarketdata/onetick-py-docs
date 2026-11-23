# otp.AccessInfo

### ``class AccessInfo(info_type='databases', , deep_scan=False, show_for_all_users=False, symbol=utils.adaptive, db=utils.adaptive, tick_type=utils.adaptive, start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Shows access information of different OneTick components.
Different options suggest different components.
All output ticks have the timestamp of the query start time.

Output: A tick for each entry of each component.

* **Parameters:**
  * **info_type** (*str*) – 

    This parameter specifies the component to get access information about.
    Possible options are `databases`, `databases_including_derived`, `features`,
    `event_processors`, `resources`, `variables`, `paths`, and `roles`:

    `databases`
    : If the `show_for_all_users` option is not specified,
      then EP shows the list of databases to which the user has access.
      In this case, if the `deep_scan` is also set, the output ticks have the following fields
      to indicate the access level for each database on each host, for each applicable time interval:
      
      **DB_NAME**, **READ_ACCESS**, **WRITE_ACCESS**, **MIN_AGE_SET**, **MIN_AGE_MSEC**,
      **MAX_AGE_SET**, **MAX_AGE_MSEC**, **MIN_START_DATE_SET**, **MIN_START_DATE_MSEC**,
      **MAX_END_DATE_SET**, **MAX_END_DATE**, **MAX_QUERY_DURATION_SET**, **MAX_QUERY_DURATION**,
      **MIN_AGE_DB_DAYS**, **MAX_AGE_DB_DAYS_SET**, **CEP_ACCESS**, **MEMDB_ACCESS**,
      **SERVER_ADDRESS**, **INTERVAL_START**, **INTERVAL_END**, **GUI_VISIBLE**
      
      When `deep_scan` is not set, the output ticks have the following fields
      to indicate the access level of each database in the host where the query will run.
      
      **DB_NAME**, **READ_ACCESS**, **WRITE_ACCESS**, **MIN_AGE_SET**, **MIN_AGE_MSEC**,
      **MAX_AGE_SET**, **MAX_AGE_MSEC**, **MIN_START_DATE_SET**, **MIN_START_DATE_MSEC**,
      **MAX_END_DATE_SET**, **MAX_END_DATE**, **MAX_QUERY_DURATION_SET**, **MAX_QUERY_DURATION**,
      **MIN_AGE_DB_DAYS**, **MAX_AGE_DB_DAYS_SET**, **CEP_ACCESS**, **MEMDB_ACCESS**
      
      If the `show_for_all_users` option is specified, then the EP shows database information
      from the access control file (for all databases from access control file, and not from the locator).
      The `deep_scan` option is not allowed in this case.
      The output ticks will have the following fields to indicate the access level of each database
      for each role in the host where the query will run:
      
      **DB_NAME**, **READ_ACCESS**, **WRITE_ACCESS**, **MIN_AGE_SET**, **MIN_AGE_MSEC**,
      **MAX_AGE_SET**, **MAX_AGE_MSEC**, **MIN_START_DATE_SET**, **MIN_START_DATE_MSEC**,
      **MAX_END_DATE_SET**, **MAX_END_DATE**, **MAX_QUERY_DURATION_SET**, **MAX_QUERY_DURATION**,
      **MIN_AGE_DB_DAYS**, **MAX_AGE_DB_DAYS_SET**, **CEP_ACCESS**, **MEMDB_ACCESS**, **ROLE**

    `databases_including_derived`
    : Same as `databases`, except that output produced for this option
      also includes information for derived databases.

    `features`/`event_processors`
    : If the `show_for_all_users` option is not set,
      the EP shows the list of allowed features/event_processors for the current user.
      The following output tick fields indicate the properties and values of an item
      along with the role with which access is granted:
      
      **FEATURE_NAME**/**EP_NAME**, **PROPERTY**, **VALUE**, **ROLE**
      
      The EP also shows item level default parameters with the OTHER role name.
      In addition, the EP also adds a tick per feature/event_processor
      with PROPERTY=ACCESS, VALUE=allowed/denied, and ROLE=””.
      
      If `show_for_all_users` is set, the EP shows the FEATURES/EVENT_PROCESSORS
      specified in the access control file for all roles.
      The following output tick fields indicate the category of the parameters for each item
      along with the role with which access is granted:
      
      **FEATURE_NAME**/**EP_NAME**, **PARAMETERS**, **ROLE**
      
      For each feature and event processor listed in the access control file,
      the EP also shows the default item level parameters with the OTHER role name.
      In addition, for each event processor that is represented in the access control file
      only through its item-level entry that does not carry any item-level parameters,
      and with no role-level entries, ACCESS_INFO EP outputs a tick with the event processor’s name,
      empty value of parameters, and role NONE.

    `resources`/`variables`
    : If the `show_for_all_users` option is not set,
      the EP shows the RESOURCES/VARIABLES specified in the access control file for the current user.
      The following output tick fields indicate the category of an item and its properties and values
      along with the role with which access is granted:
      
      **RESOURCE_NAME**/**VARIABLE_NAME**, **PROPERTY**, **VALUE**, **ROLE**
      
      The EP also shows item level default parameters with the role name OTHER.
      
      If the `show_for_all_users` option is set,
      the EP shows the RESOURCES/VARIABLES specified in the access control file for all roles.
      The following output tick fields indicate the category of an item and its parameter
      along with the role with which access is granted:
      
      **FEATURE_NAME**/**EP_NAME**, **PARAMETERS**, **ROLE**
      
      For each resource, the EP also shows the default item level parameters with the role name OTHER.

    `paths`
    : Shows the directories from the CSV_FILE_PATH, OTQ_FILE_PATH and DATA_FILE_PATH config variables
      (including extra_search_path for the user, if configured in access control).
      Output tick fields are:
      * **TYPE** - possible values CSV, OTQ and DATA
      * **PATH** - path of the directory

    `roles`
    : If the `show_for_all_users` option is not set,
      the EP shows the ROLES specified in the access control file for the current user.
      Output tick fields are:
      
      **USER**, **ROLE**
      
      If the `show_for_all_users` option is set,
      the EP shows the ROLES specified in the access control file for all users.
      Output tick fields are:
      
      **USER**, **ROLE**

    `graph_tick_functions`
    : Not described in the OneTick documentation for this EP, but supported by it.
      Output fields are the same as for `features`/`event_processors`,
      with the name of the item in the **FUNCTION_NAME** field.

    Default value is `databases`.

    #### NOTE
    Output fields returned by the current OneTick builds may differ from the ones listed above.
    For example, for `databases` there is **MAX_END_DATE_MSEC** field instead of **MAX_END_DATE**,
    fields **MIN_AGE_DB_DAYS_SET**, **MAX_AGE_DB_DAYS** and **DESTROY_ACCESS** are added,
    and for `resources`/`variables` with `show_for_all_users` set
    the name of the item is in the **RESOURCE_NAME**/**VARIABLE_NAME** field.
    The schema of this source is set according to the actual output of the EP.
  * **deep_scan** (*bool*) – 

    If **True**, the EP will process a deeper scan to bring access information from each accessible host.
    It can be **True** only when `info_type` is set to `databases`.

    Default: **False**
  * **show_for_all_users** (*bool*) – 

    If **True**, the EP will show information for all roles instead of the current user.
    For more details, see its meaning in different types.

    Default: **False**
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – Symbol(s) from which data should be taken.
    If set, will override the value specified in ``otp.run``.
  * **db** (*str*) – 

    Database name to set on the OneTick’s graph node.
    By default ``otp.config.default_db`` is used.

    The output of this EP doesn’t depend on the database and the symbol,
    but OneTick needs them to run the query.
  * **tick_type** (*str*) – Tick type to set on the OneTick’s graph node.
    Default: ANY.
  * **start** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **end** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Get access information for the databases available to the current user:

```
>>> data = otp.AccessInfo()
>>> data = data[['DB_NAME', 'READ_ACCESS', 'WRITE_ACCESS', 'CEP_ACCESS', 'MEMDB_ACCESS']]
>>> otp.run(data)
          Time          DB_NAME  READ_ACCESS  WRITE_ACCESS  CEP_ACCESS  MEMDB_ACCESS
0   2003-12-01               A3            1             0           0             1
1   2003-12-01         A3_DAILY            1             0           0             1
2   2003-12-01            ABAXX            1             0           0             1
...
```

Get the list of event processors allowed for the current user:

```
>>> data = otp.AccessInfo('event_processors')
>>> otp.run(data)
        Time          EP_NAME PROPERTY    VALUE ROLE
0 2003-12-01  COMMAND_EXECUTE   ACCESS       allowed
1 2003-12-01    READ_FROM_RAW   ACCESS       allowed
2 2003-12-01    RELOAD_CONFIG   ACCESS       allowed
...
```

Get roles of all users from the access control file:

```
>>> data = otp.AccessInfo('roles', show_for_all_users=True)
>>> otp.run(data)
        Time     USER   ROLE
0 2003-12-01    user1  Admin
1 2003-12-01    user2  Admin
```

##### SEE ALSO
**ACCESS_INFO** OneTick event processor

``onetick.py.databases()``

``onetick.py.db._inspection.DB.access_info()``

