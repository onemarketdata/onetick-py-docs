# otp.ops.get_symbol_parameters

### ``get_symbol_parameters()``

Returns symbol parameters as a comma separated list of name-value pairs.

* **Return type:**
  ``Operation``

##### Examples

```
>>> symbols = otp.Tick(SYMBOL_NAME='AAPL', SYMBOL_PARAM_1=1, SYMBOL_PARAM_2='hello')
>>> data = otp.Tick(SYMBOL_PARAMETERS=otp.ops.get_symbol_parameters())
>>> result = otp.run(data, symbols=symbols)
>>> result['AAPL']
        Time                          SYMBOL_PARAMETERS
0 2003-12-01  SYMBOL_PARAM_1='1',SYMBOL_PARAM_2='hello'
```

##### SEE ALSO
**GET_SYMBOL_PARAMETERS** OneTick function

