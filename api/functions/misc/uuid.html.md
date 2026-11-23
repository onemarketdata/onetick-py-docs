# otp.ops.uuid

### ``uuid()``

Returns a unique identifier in form: `[mac_address].[timestamp].[process_id].[seq_num]`, where:

* `mac_address` - is the mac address of the machine
* `timestamp` - the current time expressed as the number of milliseconds since the UNIX epoch
* `process_id` - process ID
* `seq_num` - is a unique to a process integer that is incremented per call to this function

* **Return type:**
  ``Operation``

##### Examples

```
>>> data = otp.Tick(UUID=otp.ops.uuid())
>>> otp.run(data)
        Time                                UUID
0 2003-12-01  000000000000.1793903402585.12187.1
```

##### SEE ALSO
**UUID** OneTick function

