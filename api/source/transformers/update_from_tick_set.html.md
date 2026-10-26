# otp.Source.update_from_tick_set

#### ``Source.update_from_tick_set(tick_set, where=None, , inplace=False)``

Updates each input tick, that is matching a selection criteria,
with values from the tick set’s tick, which matches the input tick by the tick set’s key fields.

Only fields that are present both in the input tick and in the tick set are updated.
Input ticks that have no matching tick in the tick set are propagated unchanged.
The schema of the source is not changed.

* **Parameters:**
  * **tick_set** (``TickSet`` or str) – Tick set state variable, whose ticks will be used to modify the values of input ticks,
    e.g. `data.state_vars['SET']`.
    The name of the state variable can also be passed as a string.
    All key fields of the tick set must be present in the source’s schema.
  * **where** (``Operation``) – Logical expression for selection of input ticks that will be updated.
    By default, all input ticks are selected.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing. Otherwise method returns a new modified
    object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Update field **B** of the input ticks with the values from the tick set, using field **A** as a key.
Note that field **D** from the tick set is not added to the output:

```
>>> data = otp.Ticks(A=[1, 2, 3, 4], B=[10, 20, 30, 40])
>>> data.state_vars['SET'] = otp.state.tick_set(
...     'oldest', 'A', otp.eval(otp.Ticks(A=[1, 3, 5], B=[100, 300, 500], D=[1.5, 2.5, 3.5]))
... )
>>> data = data.update_from_tick_set(data.state_vars['SET'])
>>> otp.run(data)
                     Time  A    B
0 2003-12-01 00:00:00.000  1  100
1 2003-12-01 00:00:00.001  2   20
2 2003-12-01 00:00:00.002  3  300
3 2003-12-01 00:00:00.003  4   40
```

Parameter `where` can be used to update only some of the input ticks:

```
>>> data = otp.Ticks(A=[1, 2, 3, 4], B=[10, 20, 30, 40])
>>> data.state_vars['SET'] = otp.state.tick_set(
...     'oldest', 'A', otp.eval(otp.Ticks(A=[1, 3, 5], B=[100, 300, 500]))
... )
>>> data = data.update_from_tick_set(data.state_vars['SET'], where=data['B'] > 15)
>>> otp.run(data)
                     Time  A    B
0 2003-12-01 00:00:00.000  1   10
1 2003-12-01 00:00:00.001  2   20
2 2003-12-01 00:00:00.002  3  300
3 2003-12-01 00:00:00.003  4   40
```

##### SEE ALSO
``otp.state.tick_set``

**UPDATE_FROM_TICK_SET** OneTick event processor

