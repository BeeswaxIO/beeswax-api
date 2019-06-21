This tool is provided by Beeswax under the Apache 2 license as-is for the benefit of our customers and partners.

It validates the format of model manifest and predictions files. Any detected errors are printed to the console.

Installation:

tar -xvf bid_model_validator.tar
pip install -r requirements.txt

Run:

1. Make sure validate_bid_model and validate_bid_model.runfiles are
in the same directory. They are by default when you untar the archive.

2. Run
./validate_bid_model --manifest-file-path <manifest-file-path>

<manifest-file-path>: file path to bid model manifest.
NOTE: the path can be an URL(s3://bucket/path/to/file) to S3 file or a
local absolute path.
