# otp.ops.get_orig_sym_param_val

### ``get_orig_sym_param_val(name, dtype)``

For multi-stage queries returns the value for the specified symbol parameter preserving original value type.

* **Parameters:**
  * **name** (str or ``Operation``) – The name of the symbol parameter.
  * **dtype** – One of the python classes specified in `Types`.
* **Return type:**
  ``Operation``

##### Examples

```
>>> symbols = otp.Tick(SYMBOL_NAME='AAPL', SYMBOL_PARAM_1=1, SYMBOL_PARAM_2='hello')
>>> data = otp.Tick(A=1)
>>> data['SYMBOL_PARAM_1'] = otp.ops.get_orig_sym_param_val('SYMBOL_PARAM_1', int)
>>> data['SYMBOL_PARAM_2'] = otp.ops.get_orig_sym_param_val('SYMBOL_PARAM_2', str)
>>> result = otp.run(data, symbols=symbols)
>>> result['AAPL']
        Time  A  SYMBOL_PARAM_1 SYMBOL_PARAM_2
0 2003-12-01  1               1          hello
```

##### SEE ALSO
**GET_ORIG_SYM_PARAM_VAL** OneTick function

