# otp.misc.get_symbology_mapping

### ``get_symbology_mapping(dest_symbology, src_symbology=None, symbol=None, timestamp=None)``

Translates and returns the symbol in `dest_symbology` using the current timestamp as the symbol date.

The remaining optional parameters are specified to overwrite
the symbology of the current symbol, the current symbol, and the timestamp, respectively.

* **Parameters:**
  * **dest_symbology** (str, ``Operation``) – Symbology to translate the symbol name to.
  * **src_symbology** (str, ``Operation``) – Symbology from which the symbol will be translated.
    Will be taken from the input symbol name if it has symbology part in it
    or defaults to the symbology of the input database, which is specified in the locator file.
  * **symbol** (str, ``Operation``) – Used to specify the input symbol name.
    By default the symbol name of the query is used.
  * **timestamp** (``Operation``) – They symbol date to use when translating symbol name.
    By default the current timestamp of the tick is used.
* **Return type:**
  ``Operation``

##### Examples

Get the symbol name in OID symbology:

