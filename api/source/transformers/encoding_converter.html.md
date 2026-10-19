# otp.Source.encoding_converter

#### ``Source.encoding_converter(input_encoding, output_encoding, , fields=None, , inplace=False)``

Converts the values of selected target string or `varstring`
fields in each input tick to a specified `output_encoding`,
with the converted values output in `varstring` format.

#### NOTE
Popular supported encoding names are: ASCII, UTF-8, UTF-16, UTF-32, Latin-1, Windows-1252, MacRoman, ISO 8859-1.
For the full list of existing string encoding names, check the IANA Character Sets.

* **Parameters:**
  * **fields** (*str* *or* *list*) – A field name or a list of field names to convert.
    If empty, then all string fields will be converted.
  * **input_encoding** (*int*) – The encoding format for the input data.
  * **output_encoding** (*int*) – The encoding format for the output data.
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing. Otherwise method returns a new modified
    object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

Convert all string fields from UTF-8 to ASCII encoding:

```
>>> data = otp.Tick(A='español')
>>> data = data.encoding_converter('utf-8', 'ascii')
>>> otp.run(data, encoding='ascii')
        Time        A
0 2003-12-01  espaol
```

Or convert field A from UTF-8 to Latin-1:

```
>>> data = otp.Tick(A='español 🤔')
>>> data = data.encoding_converter('utf-8', 'Latin-1', ['A'])
>>> otp.run(data, encoding='Latin-1')
        Time          A
0 2003-12-01  español 
```

##### SEE ALSO
**ENCODING_CONVERTER** OneTick event processor
