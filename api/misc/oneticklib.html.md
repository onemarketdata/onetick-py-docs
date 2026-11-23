# otp.OneTickLib

### ``class OneTickLib(*args, **kwargs)``

Bases: ``object``

Singleton class for `otq.OneTickLib` to initialize it once.

Returns the same object if it was already initialized.

#### ``cleanup()``

Destroy otq.OneTickLib instance and reset singleton class

#### ``set_log_file(log_file)``

Set log file for given instance of OneTickLib

* **Parameters:**
  **log_file** – path to log file

#### ``set_logging_level(lvl)``

Logging level can be specified by using LoggingLevel Enum class

* **Parameters:**
  **lvl** (*LoggingLevel*) – available values are LoggingLevel.MIN, LoggingLevel.LOW, LoggingLevel.MEDIUM or LoggingLevel.MAX
* **Returns:**

#### ``set_authentication_token(auth_token)``

Set authentication token for given instance of OneTickLib

* **Parameters:**
  **auth_token** (*str*) – authentication token

#### ``static override_config_value(config_parameter_name, config_parameter_value)``

Override config value of OneTickConfig

* **Parameters:**
  * **config_parameter_name** (*str*) – param to override (could be both set or not set in OneTickConfig)
  * **config_parameter_value** – new value of the param

#### ``static enable_crash_stacks(file=sys.stderr, log_link=None)``

Report both stacks when the process crashes (SIGSEGV, SIGBUS, SIGABRT) inside OneTick:
``faulthandler`` writes the Python traceback to `file`,
OneTick writes the C++ stack to its log file.

Call it from the main thread before the OneTickLib object is constructed.
On platforms other than Linux and in WebAPI mode it only enables ``faulthandler``.

* **Parameters:**
  * **file** – file object or file descriptor for the Python traceback
  * **log_link** – path of a symbolic link to keep pointing to the current OneTick log file,
    which for ``otp.Session`` is a temporary file.
    The link is removed when the OneTickLib object is destroyed, so it is left only if the process dies.
