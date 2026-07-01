# otp.delete_cache

### ``delete_cache(cache_name, apply_to_entire_cache=True, per_cache_otq_params=None, tick_type='ANY', symbol=None, db=None)``

Delete cache via DELETE_CACHE EP

* **Parameters:**
  * **cache_name** (*str*) – Name of the cache to be deleted.
  * **apply_to_entire_cache** (*bool*) – When set to `True` deletes the cache for all symbols and time intervals.
  * **per_cache_otq_params** (*dict*) – Deletes cache that have been associated with this OTQ parameters during its creation.
    Value of this parameter should be equal to the value of `otq_params` of
    `<onetick.py.create_cache>()`.
