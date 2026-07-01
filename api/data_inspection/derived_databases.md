# otp.derived_databases

### ``derived_databases(context=utils.default, start=None, end=None, selection_criteria='all', db=None, db_discovery_scope='query_host_only', as_table=False, query_properties=None)``

Gets available derived databases.

* **Parameters:**
  * **context** (*str* *,* *optional*) – Context to run the query.
    If not set then default ``context`` is used.
    See `guide about switching contexts` for examples.
  * **start** (``otp.datetime``, optional) – 

    If both `start` and `end` are set, then listing databases in this range only.
    Otherwise list databases from all configured time ranges for databases.

    If `db` is set, then
    ``otp.config.default_start_time``
    is used by default.
  * **end** (``otp.datetime``, optional) – 

    If both `start` and `end` are set, then listing databases in this range only.
    Otherwise list databases from all configured time ranges for databases.

    If `db` is set, then
    ``otp.config.default_end_time`` is used by default.
  * **selection_criteria** (*str*) – Possible values: *all*, *derived_from_current_db*, *direct_children_of_current_db*.
