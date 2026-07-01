# otp.utils.TmpDir

### ``class TmpDir(rel_path='', *, suffix='', clean_up=default, base_dir=default)``

Bases: ``PathLike``, `CleanUpFinalizer`

Class to create a temporary directory.
By default, this directory will be deleted automatically after python process exits.
All files and directories under this one will be deleted too.

