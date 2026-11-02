# otp.ops.name_value_pair_remove

### ``name_value_pair_remove(name, , pairs)``

Remove `name=value` pair from a comma-separated list of `pairs`.

* **Parameters:**
  * **name** (str, ``Operation``)
  * **pairs** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Removing the pair from a list of pairs:

```
>>> data = otp.Tick(A='a=1,b=2')
>>> data['B'] = otp.ops.name_value_pair_remove('a', data['A'])
>>> otp.run(data)
        Time        A    B
0 2003-12-01  a=1,b=2  b=2
```

##### SEE ALSO
**NAME_VALUE_PAIR_REMOVE** OneTick function

``name_value_pair_add()``

``name_value_pair_modify()``

