|Header                       |Position|Definition|SQL Datatype |DDL Desc                       |
|-----------------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------|
|account_id |1 |Beeswax bidder account ID; represents the bidder seat for a particular client |INT4 ||
|auction_adgroup_id |2 |Unique ID for every conversion in the system; system set |VARCHAR(255) |                               |
|auction_id |3 |Unique ID for every bid request in the system. A joining key for all the events associated with the bid request, like impression, clicks, and activities  |VARCHAR(255) |      |
|bid_time_utc |4 |Time of bid request sent, in UTC timezone |TIMESTAMP    |YYYY-MM-DD HH24:MI:SS.MS in ET |                               
|buzz_key |5 |Beeswax Buzz key, an identifier for client bidder instances |VARCHAR(255) |
|campaign_id |6 |ID of the campaign that submitted the bid	 |INT8 |  |
|currency_code |7 |Three letter currency codes setup in buzz |VARCHAR(10) |                               |
|line_item_id |8 |Line Item ID that was responsible for winning the auction, as listed in Beeswax	|INT8 |                               |
|vendor_fee_currency_code |9 |Currency code for vendor_fee_micros	 |VARCHAR(10) |                               |
|vendor_fee_micros |10 |Vendor fee amount in the currency set in the UI/specific to the fee |INT8         |                               |
|vendor_fee_micros_usd |11 |Vendor fee amount in USD  |INT8    ||
|vendor_id |12 |ID of the vendor (set in the UI for custom fees) |INT8|                               |
|vendor_name |13 |Name of the vendor |VARCHAR(255) |   |
|vendor_type |14 |Denotes whether fee is custom (CUSTOMER) or a standard  3P fee (DATA_PROVIDER) |VARCHAR(50) |                               |
|merged_vendor_fee_id |15 |Primary key and unique ID for each fee	 |VARCHAR(255) |                               |
