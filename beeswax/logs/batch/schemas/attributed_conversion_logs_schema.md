|Header                       |Position|Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |SQL Datatype |DDL Desc                       |
|-----------------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------|
|account_id                   |1       |Beeswax bidder account ID; represents the bidder seat for a particular client                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |INT8         |                               |
|advertiser_id                |2       |Advertiser ID for the conversion                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |INT8         |                               |
|auction_id                   |3       |Unique ID for every bid request in the system. A joining key for all the events associated with the bid request, like impression, clicks, and activities.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |VARCHAR(255) |                               |
|bid_time                     |4       |Time of the conversion's associated bid request on the attributed auction, YYYY-MM-DD HH:MM:SS in ET timezone                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |TIMESTAMP    |YYYY-MM-DD HH24:MI:SS.MS in ET |
|bid_time_utc                 |5       |Time of the conversion's associated bid request on the attributed auction, YYYY-MM-DD HH:MM:SS in UTC timezone                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |TIMESTAMP    |YYYY-MM-DD HH24:MI:SS.MS in UTC|
|buzz_key                     |6       |Beeswax Buzz key, an identifier for client bidder instances                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |VARCHAR(255) |                               |
|conversion_id                |7       |Unique ID for every conversion in the system; system set                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |VARCHAR(255) |                               |
|conversion_ord               |8       |Random number used as a cachebuster to track multiple conversions. Set by client                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |VARCHAR(255) |                               |
|conversion_order             |9       |The number of items purchased as part of the conversion. If provided as a string in the initial request, it will be coerced to 1. See conversion_order_raw for the alternative.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |VARCHAR(255) |                               |
|rx_timestamp                 |10      |Conversion received time in ET Timezone                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |TIMESTAMP    |YYYY-MM-DD HH24:MI:SS.MS in ET |
|rx_timestamp_utc             |11      |Conversion received time in UTC Timezone                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |TIMESTAMP    |YYYY-MM-DD HH24:MI:SS.MS in UTC|
|event_id                     |12      |The Event ID for the conversion being reported. This is associated with an Event Name (specific conversion event)  in the client bidder, and is set by the client                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |INT8         |                               |
|conversion_value             |13      |The value assigned to the conversion. If provided as a string in the initial request, the default value on Event is used instead. See conversion_value_raw for the alternative.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |NUMERIC(18,6)|                               |
|create_time_utc              |14      |Time created; Beeswax internal bookkeeping field                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |TIMESTAMP    |YYYY-MM-DD HH24:MI:SS.US in UTC|
|conversion_type              |15      |Signifies whether the conversion was attributed via Postback or Non-Postback                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |VARCHAR(255) |                               |
|campaign_id                  |16      |If using event assignment for attribution, the campaign ID of the campaign receiving attribution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |INT8         |                               |
|line_item_id                 |17      |If using event assignment for attribution, the line item ID of the line item receiving attribution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |INT8         |                               |
|attribution_method           |18      |The methodology used to attribute the conversion, can be "VIEWTHROUGH," "CLICKTHROUGH,", "POSTBACK" or "SKADNETWORK"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |VARCHAR(255) |                               |
|test_group_id                |19      |ID of the Test Group the user fell into within the test plan. Should match the Test Group assigned to the line item                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |INT4         |                               |
|experiment_user_index        |20      |Random number between 1-1000 assigned to a user. Used for test group assignment                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |INT4         |                               |
|test_plan_id                 |21      |ID of the Test Plan associated with the campaign                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |INT4         |                               |
|app_bundle                   |22      |Application bundle or package name (e.g., com.foo.mygame). This is intended to be a unique ID across multiple exchanges.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |VARCHAR(255) |                               |
|creative_id                  |23      |Beeswax ID for the creative that won the associated impression.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |INT4         |                               |
|postback_url                 |24      |When the Conversion was sent to Beeswax via Postback, this field will populate the requested URL.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |VARCHAR(1024)|                               |
|conversion_order_raw         |25      |The raw value passed to Beeswax in the Order field. This field does not undergo coercion to a numeric data type in attribution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |VARCHAR(1024)|                               |
|conversion_value_raw         |26      |The raw value passed to Beeswax in the Value field. This field does not undergo coercion to a numeric data type in attribution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |VARCHAR(1024)|                               |
|geo_city                     |27      |City geo code IP address. MaxMindDB Lookup data                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |VARCHAR(255) |                               |
|geo_country                  |28      |Country geo name IP address. MaxMindDB Lookup data                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |VARCHAR(255) |                               |
|geo_metro                    |29      |Metro geo code IP address. MaxMindDB Lookup data                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |VARCHAR(255) |                               |
|geo_region                   |30      |Geo region name IP address. MaxMindDB Lookup data                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |VARCHAR(255) |                               |
|geo_zip                      |31      |Zip code IP address. MaxMindDB Lookup data                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |VARCHAR(255) |                               |