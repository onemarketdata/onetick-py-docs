# otp.utils.TmpFile

### ``class TmpFile(suffix='', name='', clean_up=default, force=False, base_dir=default)``

Bases: `File`, ``PathLike``, `CleanUpFinalizer`

Class to create a temporary file.
By default, this file will be deleted automatically after python process exits.
