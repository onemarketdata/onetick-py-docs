# otp.Operation.str.substr

### ``substr(start, n_bytes=None, rtrim=False)``

Return `n_bytes` characters starting from `start`.

For a positive `start` return `num_bytes` of the string, starting from the position specified by
`start` (0-based).
For a negative `start`, the position is counted from the end of the string.
If the `n_bytes` parameter is omitted, returns the part of the input string
starting at `start` till the end of the string.

* **Parameters:**
