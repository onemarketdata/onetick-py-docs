# otp.modify_cache_config

### ``modify_cache_config(cache_name, param_name, param_value, tick_type='ANY', symbol=None, db=None)``

Modify cache configuration via MODIFY_CACHE_CONFIG EP

* **Parameters:**
  * **cache_name** (*str*) – Name of the cache to be deleted.
  * **param_name** (*str*) – 

    The name of the configuration parameter to be changed.
    Supported parameters:
    * `inheritability`
    * `time_granularity`
    * `time_granularity_units`
    * `timezone`
    * `allow_search_to_everyone`
    * `allow_delete_to_everyone`
    * `allow_update_to_everyone`
  * **param_value** (*Any*) – New value of configuration parameter. Will be converted to string.
  * **tick_type** (*str*) – Tick type.
  * **symbol** (str, list of str, list of otq.Symbol, ``onetick.py.Source``, `pandas.DataFrame`, optional) – `symbols` parameter of `otp.run()`.
  * **db** (*str*) – Database.
