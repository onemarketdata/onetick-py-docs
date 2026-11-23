# otp.ops.get_tick_server_client_announcements_file

### ``get_tick_server_client_announcements_file()``

Returns the content of the client announcements file specified in
*TICK_SERVER_CLIENT_ANNOUNCEMENTS_FILE* configuration parameter in OneTick configuration file.

* **Return type:**
  ``Operation``

##### Examples

```
>>> client_announcements_file = otp.utils.TmpFile()
>>> with open(client_announcements_file, 'w') as f:
...     f.write('Hello!')
>>> s = otp.Session(
...     otp.Config(variables={
...         'TICK_SERVER_CLIENT_ANNOUNCEMENTS_FILE': str(client_announcements_file)
...     })
... )
>>> data = otp.Tick(CLIENT_ANNOUNCEMENTS_FILE=otp.ops.get_tick_server_client_announcements_file())
>>> otp.run(data, symbols='LOCAL::')
        Time  CLIENT_ANNOUNCEMENTS_FILE
0 2003-12-01                     Hello!
```

##### SEE ALSO
**GET_TICK_SERVER_CLIENT_ANNOUNCEMENTS_FILE** OneTick function

