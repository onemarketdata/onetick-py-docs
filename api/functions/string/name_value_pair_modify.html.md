# otp.ops.name_value_pair_modify

### ``name_value_pair_modify(name, value, , pairs)``

Modify `name=value` pair in a comma-separated list of `pairs`.

* **Parameters:**
  * **name** (str, ``Operation``)
  * **value** (str, ``Operation``)
  * **pairs** (str, ``Operation``)
* **Return type:**
  ``Operation``

##### Examples

Modifying the pair in a list of pairs:

```
>>> data = otp.Tick(A='a=1,b=2')
>>> data['B'] = otp.ops.name_value_pair_modify('a', '2', data['A'])
>>> otp.run(data)
        Time        A        B
0 2003-12-01  a=1,b=2  a=2,b=2
```

##### SEE ALSO
**NAME_VALUE_PAIR_MODIFY** OneTick function

``name_value_pair_add()``

``name_value_pair_remove()``

