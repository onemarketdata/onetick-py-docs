

# WebAPI with on-prem OneTick server

## Prerequisites

- You installed OneTick and have an active license. The OneTick server is already configured and running.
- OneTick server version no older than Release 1.24 (patch 20240708171408) or weekly build `20240821`.
- Users have installed `python 3.10 or newer` and `pip`

## OneTick server-side configuration

OneTick server is configured with ONE_TICK_CONFIG variable, which points to the configuration file (e.g., onetick.cfg).
The configuration file should contain the following lines:

