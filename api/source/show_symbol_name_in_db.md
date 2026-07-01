# otp.Source.show_symbol_name_in_db

#### ``Source.show_symbol_name_in_db(inplace=False)``

Adds the **SYMBOL_NAME_IN_DB** field to input ticks,
indicating the symbol name of the tick in the database.

* **Parameters:**
  * **inplace** (*bool*) – The flag controls whether operation should be applied inplace or not.
    If `inplace=True`, then it returns nothing.
    Otherwise method returns a new modified object.
  * **self** (*Source*)
* **Return type:**
  ``Source`` or `None`

##### Examples

For example, it can be used to display
