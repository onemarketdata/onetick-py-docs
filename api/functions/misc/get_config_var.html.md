# otp.ops.get_config_var

### ``get_config_var(name)``

Returns the value of the configuration parameter specified in the OneTick configuration file.

Returns empty string if such a parameter is absent in the OneTick configuration file.

* **Parameters:**
  **name** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(
...     ALLOW_ENV_VARS=otp.ops.get_config_var('ONE_TICK_CONFIG.ALLOW_ENV_VARS'),
...     DB_LOCATOR_DEFAULT=otp.ops.get_config_var('DB_LOCATOR.DEFAULT'),
... )
>>> otp.run(data)
        Time  ALLOW_ENV_VARS                            DB_LOCATOR_DEFAULT
0 2003-12-01             Yes  /tmp/test_user/run_20261105_191931_10044/...
```

##### SEE ALSO
**GET_CONFIG_VAR** OneTick function

