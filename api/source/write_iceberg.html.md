# otp.Source.write_iceberg

#### ``Source.write_iceberg(, catalog_config, table_identifier, output_path, compression_type='snappy', memory_threshold=50, propagate_input_ticks=False, fields_for_disabled_dictionary_encoding=None, inplace=False)``

Writes the input tick series into an existing Iceberg table specified by `table_identifier`,
using the catalog settings provided in the `catalog_config` file.

The ticks are written as parquet data files, which are then registered with the Iceberg catalog.
The creation and writing of the parquet files is delegated to
an internal ``write_parquet()`` method.

* **Parameters:**
  * **catalog_config** (*str*) – Path to a configuration file containing the Iceberg catalog parameters.
    For details on the file structure and how it is processed, see Examples below.
  * **table_identifier** (*str*) – The Iceberg table identifier, including the namespace and table name (for example, `namespace.tablename`).
    The table must already exist.
  * **output_path** (*str*) – The output location for the parquet data files.
    This value is passed through to the internal ``write_parquet()`` method;
    see its `output_path` parameter for the supported path handling
    (writing to a directory or directly to a single file).
  * **compression_type** (*str*) – Compression algorithm used when writing the parquet files.
    Supported values: gzip, lz4, none, snappy (default), zstd.
  * **memory_threshold** (*float*) – How much, in megabytes, is buffered per thread before ticks are passed to be written.
    Default: 50
  * **propagate_input_ticks** (*bool*) – If True then ticks will be propagated after this method.
    If False (default) this method won’t return ticks.
  * **fields_for_disabled_dictionary_encoding** (*list*) – 

    List of fields for which dictionary encoding should be disabled.
    By default, dictionary encoding is enabled for all fields.

    #### NOTE
    This parameter can only be used when the table is partitioned.
  * **inplace** (*bool*) – A flag controls whether operation should be applied inplace.
    If `inplace=True`, then it returns nothing. Otherwise method
    returns a new modified object.
  * **self** (*Source*)

#### NOTE
This method requires Java 17 or higher to be installed.
Also Java library path should be added to **PATH** (Windows) or **LD_LIBRARY_PATH** (Linux) environment variables
and to **OMD_JAVALIBPATH** OneTick config variable.

##### Examples

Write Iceberg catalog configuration first:

```
>>> with open('catalog.cfg', 'w') as f:
...     f.write('''
...         catalog.name=rest_catalog
...         type=rest
...         uri=http://localhost:8181
...         warehouse=s3://warehouse/
...         s3.region=us-east-1
...         client.region=us-east-1
...         s3.path-style-access=true
...         s3.access-key-id=admin
...         s3.secret-access-key=password
...         io-impl=org.apache.iceberg.aws.s3.S3FileIO
...         s3.delete.enabled=true
...         s3.acceleration-enabled=false
...     ''')
```

Then run the query:

```
>>> data = otp.Tick(A=1)
>>> data = data.write_iceberg(catalog_config='catalog.cfg',
...                           table_identifier='reporting.sales_data',
...                           output_path='sales')
>>> otp.run(data)
```

##### SEE ALSO
**WRITE_TO_ICEBERG** OneTick event processor

