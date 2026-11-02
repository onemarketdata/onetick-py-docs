# ETF

This section contains 4 examples for ETF using the `onetick-py`.<br />
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

## ETF Cash

Query `OQD_ETF` cash flow data for `SPY` using Bloomberg symbology.<br />
\\\\
Returns first 100 cash flow records for specified time range.

```
import onetick.py as otp

# Define the data source for OQD_ETF.CASH
source = otp.DataSource(
    db='OQD_ETF',            # OQD ETF database
    tick_type='CASH',        # Cash flow tick type
    schema_policy='manual',  # Manually define schema
    schema=None,             # Retrieve all available columns
)

# Limit to first 100 rows
source = source.limit(100)

# Define the time range in UTC
start_time = otp.dt(2024, 7, 8, tz='UTC')  # Start: July 8, 2024 at 00:00 UTC
end_time = otp.dt(2024, 8, 9, tz='UTC')    # End: August 9, 2024 at 00:00 UTC

# Run the query using Bloomberg symbol (BTKR symbology)
result = otp.run(
    source,                       # Cash flow data source
    symbols='BTKR::::SPY US',     # SPY in Bloomberg symbology
    symbol_date=end_time,         # Date for symbology mapping
    start=start_time,             # Query start time
    end=end_time,                 # Query end time
    timezone='America/New_York',  # Use New York timezone
)

result  # Display results
```

## ETF Constituents

Query `OQD_ETF` constituent holdings for `SPY`.<br />
\\\\
Returns first 100 constituents as of August 9, 2024 using Bloomberg symbology.

```
import onetick.py as otp

# Define the data source for ETF constituents
constituents = otp.DataSource(
    db='OQD_ETF',              # OQD ETF database
    tick_type='CONSTITUENTS',  # ETF constituents tick type
    schema_policy='manual',    # Manually define schema
    schema=None,               # Retrieve all available columns
)

# Limit to first 100 rows (optional)
constituents = constituents.limit(100)

# Define the time range in UTC
start_time = otp.dt(2024, 7, 8, tz='UTC')  # Start: July 8, 2024
end_time = otp.dt(2024, 8, 9, tz='UTC')    # End: August 9, 2024

# Define the symbol date (as of date for constituent holdings)
symbol_date=otp.dt(2024, 8, 9, tz='UTC')  # Get constituents as of August 9, 2024

# Run the query for SPY constituents using Bloomberg symbol
result = otp.run(
    constituents,                 # ETF constituents data source
    symbols='BTKR::::SPY US',     # SPY in Bloomberg symbology
    symbol_date=symbol_date,      # Date for constituent snapshot
    start=start_time,             # Query start time
    end=end_time,                 # Query end time
    timezone='America/New_York',  # Use New York timezone
)

result  # Display results
```

## ETF PCF

Query `OQD_ETF` portfolio composition (`PCF`) data for `SPY`.<br />
\\\\
Returns portfolio holdings and composition details using Bloomberg symbology.

```
import onetick.py as otp

# Define the time range
start = otp.dt(2024, 8, 8)  # Start: August 8, 2024 at midnight
end = otp.dt(2024, 8, 9)    # End: August 9, 2024 at midnight

# Define the PCF data source
pcf_data = otp.DataSource(
    db='OQD_ETF',     # OQD ETF database
    tick_type='PCF',  # Portfolio Composition File tick type
)

# Run the query using Bloomberg symbology with symbol_date
symbol_date=otp.dt(2024, 8, 8)  # Date for symbology mapping
result = otp.run(
    pcf_data,                     # Portfolio composition data source
    symbols='BTKR::::SPY US',     # SPY in Bloomberg symbology
    symbol_date=symbol_date,      # Date for symbol resolution
    start=start,                  # Query start time
    end=end,                      # Query end time
    timezone='America/New_York',  # Use New York timezone
)

result  # Display results
```

## ETF Universe

Query `OQD_ETF` description/reference data for all `ETF` symbols.<br />
\\\\
Returns all available `ETF` symbol descriptions and metadata.

```
import onetick.py as otp

# Define the time range
start = otp.dt(2024, 8, 8)  # Start: August 8, 2024 at midnight
end = otp.dt(2024, 8, 9)    # End: August 9, 2024 at midnight

symbols = otp.Symbols(
    db='OQD_ETF',         # OQD ETF database
    pattern='%',          # Pattern mask to match all symbols
    for_tick_type='DES',  # For DES (description) tick type
)

# Define the DES data source containing reference/description data for ETF symbols
des_data = otp.DataSource(
    db='OQD_ETF',     # OQD ETF database
    tick_type='DES',  # Description/reference data tick type
)

# merge all ETF symbols into one stream
des_data = otp.merge([des_data], symbols=symbols, identify_input_ts=True)

# Return first 100 Rows
des_data = des_data.limit(100)

# Run the query
result = otp.run(
    des_data,                     # Description data source
    start=start,                  # Query start time
    end=end,                      # Query end time
    timezone='America/New_York',  # Query timezone
)

result  # Display results
```
