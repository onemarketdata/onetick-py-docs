

# Ray client installation

**DEPRECATED** - this section is deprecated and will be removed in the future. Please, consider using the WebAPI instead, details `here`.

This section describes installation and configuration of Ray client, which is necessary to run `onetick.py` code remotely on a Ray instance.
You don’t need it, if you use `onetick.py` locally with fully installed OneTick, as mentioned above.

#### NOTE
Commands in this guide are expected to be run on Linux.
Some changes must be made to run them on Windows.
For example, on Windows `export` command should be replaced with `set` and quotes should not be used.

Ask your OneMarketData rep for a username and password, also ask for onetick-py version in your environment (ex: 1.62.1).
Then run the commands below (replacing USERNAME, PASSWORD and OTP_VERSION with your values):

```
pip install -U --index-url https://USERNAME:PASSWORD@pip.distribution.sol.onetick.com/simple/ onetick-query-stubs[ray23] onetick-py==OTP_VERSION
export OTP_SKIP_OTQ_VALIDATION=1
```

If your server instance have Ray 2.9 or higher, use `onetick-query-stubs[ray29]` instead of `onetick-query-stubs[ray23]` in the command above.

To simplify Ray initialization in the future, add a new environment variable with Ray instance URL (ask your OneMarktData rep):

```
export RAY_ADDRESS="ray://<URL>:10001"
```

Now you can start coding in your IDE and you could do `import onetick.py` as well.
But you can’t run your code locally, because you don’t have OneTick installed.

To run your code remotely on Ray, proceed to `Remote OTP with Ray` for details.



## Connection to Ray
