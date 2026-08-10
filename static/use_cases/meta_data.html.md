# Meta Data

This section contains 5 examples for Meta Data using the `onetick-py`.<br />
\\\\
Each example is a self-contained script that can be run against the OneTick Cloud sample databases.

```
# onetick-py WebAPI configuration for OneTick Cloud
import os
os.environ['OTP_WEBAPI'] = '1'
os.environ['OTP_HTTP_ADDRESS'] = 'https://rest.cloud.onetick.com'
os.environ['OTP_ACCESS_TOKEN_URL'] = 'https://cloud-auth.parent.onetick.com/realms/OMD/protocol/openid-connect/token'
os.environ['OTP_CLIENT_ID'] = '__FILL_IN__'
os.environ['OTP_CLIENT_SECRET'] = '__FILL_IN__'
```

## DB List

Use ``otp.databases`` to retrieve the list of available databases, and filter on the first 5.

```
import onetick.py as otp

data = otp.databases()
list(data)[:5]
```

## DB Symbol List

Use ``otp.Symbols`` to retrieve the list of available symbols for a given database.

```
import onetick.py as otp

data = otp.Symbols(db='US_COMP_SAMPLE')
result = otp.run(data,
                 start=otp.dt(2024, 1, 2),
                 end=otp.dt(2024, 1, 3),
                 timezone='America/New_York')
result
```

## Field Schema

Retrieve the schema from a specified data source where the database and tick type are selected.

```
import onetick.py as otp

data = otp.DataSource(db='US_COMP_SAMPLE', tick_type='TRD', symbols='CSCO',
                      start=otp.dt(2024, 1, 3), end=otp.dt(2024, 1, 4))
data.schema
```

## Masked DB Symbol List

Apply a pattern using the wildcard `%` to retrieve all symbols starting with `C`
with ``otp.Symbols``.

```
import onetick.py as otp

data = otp.Symbols(db='US_COMP_SAMPLE', pattern='C%')
result = otp.run(data,
                 start=otp.dt(2024, 1, 2),
                 end=otp.dt(2024, 1, 3),
                 timezone='America/New_York')
result
```

## Tick Type - Table List

Retrieve the list of databases, and then for a specified database, retrieve the available tick types / tables.

```
import onetick.py as otp

dbs = otp.databases()
result = dbs['US_COMP_SAMPLE'].tick_types()
result
```
