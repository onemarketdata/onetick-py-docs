# otp.ACL

### ``class ACL(path=None, clean_up=utils.default, copy=True, session_ref=None)``

Bases: `_FileHandler`

Class representing OneTick database access list file.

ACL is the file that describes the list of the users
that are allowed to access the database and what permissions do they have.

This object can be used when creating ``otp.Config`` object.

* **Parameters:**
  * **path** (*str*) – 

    A path to custom acl file.

    Default is None, which means to generate ACL file automatically.
    It will include current user with permissions to execute EPs and read/write databases.
  * **clean_up** (*bool*) – 

    If True, then temporary acl file will be removed when ACL object is destroyed. It is
    helpful for debug purposes.

    By default,
    ``otp.config.clean_up_tmp_files`` is used.
  * **copy** (*bool*) – If True, then the passed custom acl file by the `path` parameter will be copied first before
    usage. It might be used when you want to work with a custom acl file, but don’t want to change
    the original file; in that case a custom acl file will be copied into a temporary file and
    every request for modification will be executed for that temporary file. Default is True.

##### Examples

ACL object can be created with existing path:

```
>>> acl = otp.ACL('/path/to/the/acl')
```

Or it can be created automatically with some default values:

```
>>> acl = otp.ACL()
>>> acl.path
'/tmp/test_username/run_20260722_145505_4775/feathered-dragon.acl'
```

##### SEE ALSO
``otp.Session``
``otp.Config``
``otp.Locator``

#### ``add(*entities)``

Add entities to the ACL and reload it.
If it fails, then tries to roll back to the original state.

* **Parameters:**
  **entities** (``otp.DB`` or ACL.User)
* **Raises:**
  **TypeError****,** **EntityOperationFailed** – 

#### ``remove(*entities)``

Remove entities from the ACL and reload it.
If it fails, then tries to roll back to the original state.

* **Parameters:**
  **entities** (``otp.DB`` or ACL.User)
* **Raises:**
  **ValueError****,** **TypeError****,** **EntityOperationFailed** –
