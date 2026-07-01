# otp.RefData

### ``class RefData(ref_data_type=None, symbol=utils.adaptive, db=utils.adaptive_to_default, start=utils.adaptive, end=utils.adaptive, query_parameters=None, **kwargs)``

Bases: ``Source``

Shows reference data for the specified security and reference data type.

It can be used to view corporation actions,
symbol name changes,
primary exchange info and symbology mapping for a securities,
as well as the list of symbologies,
names of custom adjustment types for corporate actions present in a reference database
as well as names of continuous contracts in database symbology.

* **Parameters:**
  * **ref_data_type** (*str*) – 

    Type of reference data to be queried. Possible values are:
    * corp_actions
    * symbol_name_history
    * primary_exchange
    * symbol_calendar
    * symbol_currency
    * symbology_mapping
    * symbology_list
    * custom_adjustment_type_list
    * all_calendars
    * all_continuous_contract_names
  * **symbol** (str, list of str, ``Source``, ``query``, ``eval query``) – Symbol(s) from which data should be taken.
  * **db** (*str*) – Name of the database.
  * **start** (``otp.datetime``) – Start time for tick generation. By default the start time of the query will be used.
  * **end** (``otp.datetime``) – End time for tick generation. By default the end time of the query will be used.
  * **query_parameters** (``otp.QueryParameters``) – Additional query properties to be set in the resulting .otq file.
    They will be used if they are not overridden by other parameters or in ``otp.run``.

##### Examples

Show calendars for a database US_COMP_SAMPLE:
