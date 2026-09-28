# otp.Source

### *class* Source

Bases: ``object``

Base class for representing Onetick execution graph.
All `onetick-py sources` are derived from this class
and have access to all its methods.

##### Examples

```
>>> data = otp.Tick(A=1)
>>> isinstance(data, otp.Source)
True
```

Also this class can be used to initialize raw source
with the help of `onetick.query` classes, but
it should be done with caution as the user is required to set
such properties as symbol name and tick type manually.

```
>>> data = otp.Source(otq.TickGenerator(bucket_interval=0, fields='long A = 123').tick_type('TT'))
>>> otp.run(data, symbols='LOCAL::')
        Time    A
0 2003-12-04  123
```

* **Parameters:**
  **query_parameters** (*QueryParameters*)

## Table Of Contents

* `otp.Source.Symbol`
* otp.Source._\_call_\_
* otp.Source._\_getitem_\_
* otp.Source._\_setitem_\_
* `otp.Source.add_fields`
* `otp.Source.add_prefix`
* `otp.Source.add_suffix`
* `otp.Source.agg`
* `otp.Source.apply`
* `otp.Source.cache`
* `otp.Source.character_present`
* `otp.Source.copy`
* `otp.Source.corp_actions`
* `otp.Source.correct_tick_filter`
* `otp.Source.count (jupyter)`
* `otp.Source.deepcopy`
* `otp.Source.diff`
* `otp.Source.distinct`
* `otp.Source.drop`
* `otp.Source.dropna`
* `otp.Source.dump`
* `otp.Source.estimate_ts_delay`
* `otp.Source.execute`
* `otp.Source.exp_tw_average`
* `otp.Source.exp_w_average`
* `otp.Source.fillna`
* `otp.Source.find_value_for_percentile`
* `otp.Source.first`
* `otp.Source.get_name`
* `otp.Source.head (jupyter)`
* `otp.Source.high`
* `otp.Source.high_time`
* `otp.Source.if_else`
* `otp.Source.implied_vol`
* `otp.Source.insert_at_end`
* `otp.Source.insert_data_quality_event`
* `otp.Source.insert_tick`
* `otp.Source.intercept_data_quality`
* `otp.Source.intercept_symbol_errors`
* `otp.Source.join_with_collection`
* `otp.Source.join_with_query`
* `otp.Source.join_with_snapshot`
* `otp.Source.last`
* `otp.Source.lee_and_ready`
* `otp.Source.limit`
* `otp.Source.linear_regression`
* `otp.Source.logf`
* `otp.Source.low`
* `otp.Source.low_time`
* `otp.Source.meta_fields`
* `otp.Source.mkt_activity`
* `otp.Source.modify_query_times`
* `otp.Source.modify_symbol_name`
* `otp.Source.multi_portfolio_price`
* `otp.Source.ob_num_levels`
* `otp.Source.ob_size`
* `otp.Source.ob_snapshot`
* `otp.Source.ob_snapshot_flat`
* `otp.Source.ob_snapshot_wide`
* `otp.Source.ob_summary`
* `otp.Source.ob_vwap`
* `otp.Source.option_price`
* `otp.Source.partition_evenly_into_groups`
* `otp.Source.percentile`
* `otp.Source.plot (jupyter)`
* `otp.Source.pnl_realized`
* `otp.Source.point_in_time`
* `otp.Source.portfolio_price`
* `otp.Source.primary_exch`
* `otp.Source.print_otq`
* `otp.Source.process_by_group`
* `otp.Source.ranking`
* `otp.Source.rename`
* `otp.Source.render`
* `otp.Source.render_otq`
* `otp.Source.return_ep`
* `otp.Source.save_snapshot`
* `otp.Source.schema`
* `otp.Source.script`
* `otp.Source.set_name`
* `otp.Source.show_corrected_ticks`
* `otp.Source.show_data_quality`
* `otp.Source.show_hidden_ticks`
* `otp.Source.show_symbol_errors`
* `otp.Source.show_symbol_name_in_db`
* `otp.Source.sink`
* `otp.Source.skip_bad_tick`
* `otp.Source.sort`
* `otp.Source.split`
* `otp.Source.standardized_moment`
* `otp.Source.state_vars`
* `otp.Source.switch`
* `otp.Source.table`
* `otp.Source.tail (jupyter)`
* `otp.Source.throw`
* `otp.Source.time_filter`
* `otp.Source.time_interval_change`
* `otp.Source.time_interval_shift`
* `otp.Source.to_df`
* `otp.Source.to_graph`
* `otp.Source.to_otq`
* `otp.Source.to_symbol_param`
* `otp.Source.transpose`
* `otp.Source.update`
* `otp.Source.update_timestamp`
* `otp.Source.value_present`
* `otp.Source.virtual_ob`
* `otp.Source.where`
* `otp.Source.where_clause`
* `otp.Source.write`
* `otp.Source.write_iceberg`
* `otp.Source.write_parquet`
* `otp.Source.write_text`
