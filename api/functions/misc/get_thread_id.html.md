# otp.ops.get_thread_id

### ``get_thread_id()``

Returns the ID of the thread that is executing this function.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(THREAD_ID=otp.ops.get_thread_id())
>>> otp.run(data)
        Time        THREAD_ID
0 2003-12-01  132504766963840
```

##### SEE ALSO
**GET_THREAD_ID** OneTick function

