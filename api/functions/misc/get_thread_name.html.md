# otp.ops.get_thread_name

### ``get_thread_name()``

Returns the ID of the thread that is executing this function.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(THREAD_NAME=otp.ops.get_thread_name())
>>> otp.run(data)
        Time  THREAD_NAME
0 2003-12-01     ipython3
```

##### SEE ALSO
**GET_THREAD_NAME** OneTick function

