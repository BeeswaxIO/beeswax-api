Beeswax Win Log Requester
Generates Beeswax win logs (Impression, Click, Activity) http requests to a designated endpoint
with body generated from the specified input file. Output the http responses to a file
if specified.

Installation:

pip install -r requirements.txt
tar -xvf win_log_requester.tar

Run:

1. Make sure win_log_requester and win_log_requester.runfiles
are in the same directory. They are by default when you untar the archive.

2. Run
./win_log_requester <path-to-request-file> <bid-endpoint>

Note that step 2 assumes you have a valid endpoint running in your test environment,
which can process win logs and return responses.

<path-to-requests-file>: beeswax win logs in protobuf format.
Requests should be separated with '==='. See sample_ad_log.proto for example.
<bid-endpoint>: full url to the bid endpoint, including scheme and path.

[optional flags]
--path-to-responses-file: Response from the win logs will be written into this
file if present. The order corresponds to that in the log requests file.
--log-level: can be one of [error, info, debug]. Default to info.

Example:

./win_log_requester sample_ad_log.proto http://beeswax.bid/bid
--path-to-responses-file bid_response.txt --log-level debug
