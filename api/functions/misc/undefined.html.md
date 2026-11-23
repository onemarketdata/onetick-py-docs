# otp.ops.undefined

### ``undefined(name)``

Returns False if a state variable or a field with a given `name` was declared, and True otherwise.

* **Parameters:**
  **name** (str or ``Column`` or state variable) – If string literal is passed, this parameter is treated as a field name.
  Otherwise, ``Column`` or state variable object can be used.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(A=1)
>>> data.state_vars['B'] = 1
>>> data['UNDEFINED_A'] = otp.ops.undefined('A')
>>> data['UNDEFINED_FIELD_A'] = otp.ops.undefined(data['A'])
>>> data['UNDEFINED_STATE_VAR_B'] = otp.ops.undefined(data.state_vars['B'])
>>> data['UNDEFINED_C'] = otp.ops.undefined('C')
>>> otp.run(data)
        Time  A  UNDEFINED_A  UNDEFINED_FIELD_A  UNDEFINED_STATE_VAR_B  UNDEFINED_C
0 2003-12-01  1          0.0                0.0                    0.0          1.0
```

##### SEE ALSO
**UNDEFINED** OneTick function

