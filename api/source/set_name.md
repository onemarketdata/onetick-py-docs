# otp.Source.set_name

#### ``Source.set_name(new_name)``

Sets source name.
It’s an internal onetick-py name of the source that is only used
as a part of the resulting .otq file name and as the name of the query inside this file.

This method doesn’t set the name of the OneTick graph node.

* **Parameters:**
  **new_name** (*str*) – 

  New name of the source.

  Only alphanumeric, minus and underscore characters are supported.
  All other characters will be replaced in the resulting query name.

##### Examples

```
