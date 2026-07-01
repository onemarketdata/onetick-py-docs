

# Prerequisites

We use `pytest` as a testing framework.

If you are not familiar with it you can view a quick example by following the link above.
We chose the `pytest` framework because of:

- ease of reading and writing tests
- auto discovery feature that allows executing all available tests with a single command:
  it finds every test starting with the `test_` prefix in every subfolder.
- many useful plugins for checking memory consumption, time of execution, coverage and mocking.

Another tool that we use for testing is our `onetick-py-test` pytest plugin
that collects helpful things to ease testing and debugging with OneTick.

