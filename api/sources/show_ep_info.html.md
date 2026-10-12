# otp.ShowEpInfo

### ``class ShowEpInfo(ep_name=None, , , prefer_local_info=False, symbol=None, tick_type=None, start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Shows description for requested event processor searching all accessible tick servers.

* **Parameters:**
  * **ep_name** (*str*) – Event processor name to retrieve description for.
  * **prefer_local_info** (*bool*) – If set to True and local description is present,
    no attempt is performed to retrieve description from accessible tick servers.
    Default is False.
  * **symbol** (*str*) – Bound symbol on the node of the graph.
    Not set by default – the value from ``otp.run`` will be used.
  * **tick_type** (*str*) – Tick type set on the node of the graph.
    Not set by default.
  * **start** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **end** (``datetime.datetime``, ``otp.datetime``) – Time interval from which the data should be taken.
    Not set by default – the values from ``otp.run`` will be used.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Show information about SHOW_EP_INFO OneTick event processor:

```
>>> data = otp.ShowEpInfo('SHOW_EP_INFO')
>>> otp.run(data, symbols='LOCAL::')
        Time EVENT_PROCESSOR_NAME CATEGORY  IS_SOURCE    ORIGIN OUTPUTS_DEPENDENCY OUTPUTS       DOCUMENTATION
0 2003-12-01         SHOW_EP_INFO    Other          0  BUILT_IN   NO_NAMED_OUTPUTS          <!DOCTYPE html>...
```
