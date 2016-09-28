Beeswax Bid Requests Generator generates Beeswax bid http requests
and sends to a designated endpoint with http headers used in the biddding service
and http body generated from the specified input file.

Installation:

tar -xvf bidding_agent_requests_generator.tar
pip install -r requirements.txt


Run:

1. Make sure bid_requests_generator and bid_requests_generator.runfiles
are in the same directory. They are by default when you untar the archive.

2. Run
./bidding_agent_requests_generator <path-to-request-file> <bid-endpoint>

Note that step 2 assumes you have a valid bidder endpoint running in your test environment,
which can process bid requests and return responses.

<path-to-requests-file>: beeswax bid requests in ASCII format. Requests
should be separated with '==='. See bid_sample_request_1.txt for example.
<bid-endpoint>: full url to the bid endpoint, including scheme and path.

[optional flags]
--path-to-responses-file: Response from the bid will be written into this
file if present. The order corresponds to that in the bid requests file.
--header-secret: If present, it will be the value of secret header in http requests.
--log-level: can be one of [error, info, debug]. Default to info.

Example:

./bidding_agent_requests_generator sample_bid_request_1.txt  http://beeswax.bid/bid
--path-to-responses-file bid_response.txt --header-secret some-secret --log-level debug
