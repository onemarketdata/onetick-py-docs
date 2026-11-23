# otp.ops.get_cpu_id

### ``get_cpu_id()``

Returns the ID of the CPU core that is executing this function.

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(CPU_ID=otp.ops.get_cpu_id())
>>> otp.run(data)
        Time  CPU_ID
0 2003-12-01       9
```

##### SEE ALSO
**GET_CPU_ID** OneTick function

