# otp.ops.name_value_pair_add

### ``name_value_pair_add(name, value, , pairs=None)``

Add `name=value` pair to a comma-separated list of `pairs`.

* **Parameters:**
  * **name** (str, ``Operation``)
  * **value** (str, ``Operation``)
  * **pairs** (str, ``Operation``) – If not set, then new string is created.
* **Return type:**
  ``Operation``

##### Examples

Creating a list of pairs and adding a new pair:

```
>>> data = otp.Tick(A=otp.ops.name_value_pair_add('a', '1'))
>>> data['B'] = otp.ops.name_value_pair_add('b', '2', data['A'])
>>> otp.run(data)
        Time    A        B
0 2003-12-01  a=1  a=1,b=2
```

##### SEE ALSO
**NAME_VALUE_PAIR_ADD** OneTick function

``name_value_pair_modify()``

``name_value_pair_remove()``

