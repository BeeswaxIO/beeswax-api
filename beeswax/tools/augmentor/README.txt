Beeswax Augmentor Requests Generator generates Beeswax augmentor http requests
and sends to a designated endpoint with http headers used in the biddding service
and http body generated from the specified input file.

Installation:

pip install -r requirements.txt


Run:

1. Make sure augmentor_requests_generator and augmentor_requests_generator.runfiles
are in the same directory

2. Run
./augmentor_requests_generator <path-to-request-file> <augmentor-endpoint>

<path-to-requests-file>: beeswax augmentor requests in ASCII format. Requests
should be separated with '==='. See augmentor_sample_request_1.txt for example.
<augmentor-endpoint>: full url to the augmentor endpoint, including scheme and path.

[optional flags]
--path-to-responses-file: Response from the augmentor will be written into this
file is present. The order corresponds to that in the augmentor requests file.
--header-secret: If present, it will be the value of secret header in http requests.
--log-level: can be one of [error, info, debug]. Default to info.

Example:

./augmentor_requests_generator augmentor_sample_request_1.txt  http://beeswax.augmentor/aug
--path-to-responses-file responses.txt --header-secret some-secret --log-level debug
