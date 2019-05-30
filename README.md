# beeswax-api
Realtime API for extending the Beeswax Bidder-as-a-Service&trade;

# About Beeswax
[Beeswax](https://www.beeswax.com) offers a highly customizable and extensible RTB bidding stack we call the Bidder-as-a-Service. By utilizing Beeswax, technically sophisticated advertisers can get transparency, flexibility and control over their digital media buying.

# Documentation
Beeswax offers two types of APIs to our customers, the "Buzz" REST API for campaign trafficking and reporting, and the "Stinger" realtime APIs for responding to bid requests, augmenting bid requests with data, and otherwise integrating into our bidding system.

The REST API documentation can be found [here](http://docs.beeswax.com/docs/getting-started).

The realtime documentation can be found [here](http://docs.beeswax.com/docs/about-the-stinger-bidder).


### Maven Dependency

    <dependency>
      <groupId>com.beeswax</groupId>
      <artifactId>beeswax-api</artifactId>
      <version>2019-04-02</version>
    </dependency>


# Tools

### Augmentor requests generator

    beeswax/tools/augmentor/

generates Beeswax augmentor HTTP requests and sends them to a designated endpoint.

### Bid requests generator

    beeswax/tools/bid/

generates Beeswax bid HTTP requests and sends them to a designated endpoint.

### Win log requester

    beeswax/tools/win_events/

sends Beeswax win logs (Impression, Click, Activity) HTTP requests to a designated endpoint
with body generated from specified input file.

### Bid model validator

    beeswax/tools/bid_model_validator/

validates format of bid model manifest and prediction files and prints detected errors to the console.
