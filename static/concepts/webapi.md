# Remote access with WebAPI

WebAPI is an interface for `onetick-py` to use remote OneTick server.
It could be OneMarketData Cloud Server or on-premises OneTick server.
Main advantage of this approach is that it does not require OneTick binaries to be installed on the client side.

Installation instructions for WebAPI are available in the `Installation` section.
Also, you can find example code snippets there.

Instructions to configure your on-premise OneTick server for WebAPI are available on the `corresponding page`.

# Difference of WebAPI mode

When using WebAPI, it is not required to use `otp.Session()` object, as it makes no sense in this context.

All functions, that rely on using binaries on the client side, are not supported in WebAPI mode:

* `RefDB.put()`
* `otp.perf`

The following features are not supported when using WebAPI mode:

* `otp.Session()` object (not required)
* Ignored `otp.run()` parameters:
  : * `start_time_expression`
    * `end_time_expression`
    * `alternative_username`
    * `batch_size`
    * `treat_byte_arrays_as_strings`
    * `output_mode`
    * `output_matrix_per_field`
    * `return_utc_times`
    * `connection`
    * `svg_path`
    * `use_connection_pool`
    * `time_as_nsec`
    * `max_expected_ticks_per_symbol`
