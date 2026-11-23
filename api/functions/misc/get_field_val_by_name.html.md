# otp.ops.get_field_val_by_name

### ``get_field_val_by_name(name, dtype)``

Returns the value of a field or state variable by its `name`.

The `name` can be specified statically as a string literal
or dynamically by using columns or operations.

The `dtype` parameter specifies the type of the evaluation result.

* **Parameters:**
  * **name** (str or ``Operation``)
  * **dtype** – One of the python classes specified in `Types`.
* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Ticks(A=[1, 3], B=[2, 4], FIELD_NAME=['A', 'B'])
>>> data['FROM_A'] = otp.ops.get_field_val_by_name('A', int)
>>> data['FROM_FIELD_NAME'] = otp.ops.get_field_val_by_name(data['FIELD_NAME'], int)
>>> otp.run(data)
                     Time  A  B FIELD_NAME  FROM_A  FROM_FIELD_NAME
0 2003-12-01 00:00:00.000  1  2          A       1                1
1 2003-12-01 00:00:00.001  3  4          B       3                4
```

##### SEE ALSO
**GET_FIELD_VAL_BY_NAME** OneTick function

