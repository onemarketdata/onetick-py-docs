# otp.ops.get_type

### ``get_type(expression)``

Returns the type name of the argument.

If the argument is a tick attribute or a state variable or the operation using them.

* **Parameters:**
  **expression** (``Operation``)
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data.state_vars['TICK_LIST'] = otp.state.tick_list()
>>> data.state_vars['TICK_SET'] = otp.state.tick_set('latest', ['A'])
>>> data['A_TYPE'] = otp.ops.get_type(data['A'])
>>> data['A_DIV2_TYPE'] = otp.ops.get_type(data['A'] / 2)
>>> data['A_GT2_TYPE'] = otp.ops.get_type(data['A'] > 2)
>>> data['STR_TYPE'] = otp.ops.get_type('hello')
>>> data['TIMESTAMP_TYPE'] = otp.ops.get_type(data['TIMESTAMP'])
>>> data['TICK_LIST_TYPE'] = otp.ops.get_type(data.state_vars['TICK_LIST'])
>>> data['TICK_SET_TYPE'] = otp.ops.get_type(data.state_vars['TICK_SET'])
>>> otp.run(data)
        Time  A  A_TYPE  A_DIV2_TYPE  A_GT2_TYPE  STR_TYPE  TIMESTAMP_TYPE  TICK_LIST_TYPE  TICK_SET_TYPE
0 2003-12-01  1    long       double     boolean    string        datetime       TICK_LIST       TICK_SET
```

##### SEE ALSO
**GET_TYPE** OneTick function

