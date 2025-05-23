| Header | Position | Definition | SQL_Datatype | DDL Description |
|---|---|---|---|---|
| account_id | 1 | Beeswax bidder account ID; represents the bidder seat for a particular   client | INT4 |  |
| ad_position | 2 | If applicable, ad position on page | VARCHAR(255) |  |
| app_bundle | 3 | Application bundle or package name (e.g., com.foo.mygame). This is   intended to be a unique ID across multiple exchanges. | VARCHAR(255) |  |
| app_id | 4 | Application ID on the exchange. For uniqueness, Uses ad exchange/SSP   identifier as prefix e.g. pm/ representing pubmatic | VARCHAR(255) |  |
| app_name | 5 | Application name | VARCHAR(255) |  |
| auction_adgroup_id | 6 | Internal Unique ID | VARCHAR(255) |  |
| auction_id | 7 | Unique ID for every bid request in the system. A joining key for all the   events associated with the bid request, like impression, clicks, and   activities. | VARCHAR(255) |  |
| beeswax_fee_rate_micros | 8 | For PERCENT fee-type option, applicable Beeswax fee rate in micros 1   micro = 0.000,0001% | INT8 |  |
| bid_hour | 9 | Datestamp during which a particular bid was made, YYYY-MM-DD HH:00:00 in   ET timezone | TIMESTAMP |  |
| bid_price_micros_usd | 10 | Bid price returned by the bidding agent (in USD micros) after bid shading is applied. 1 USD = 1,000,000 micros | INT8 |  |
| bid_reduction_rate_micros | 11 | For BID_REDUCTION(rev-share) fee type option, applicable Bid reduction   rate in micros 1 micro = 0.000,0001% | INT8 |  |
| bid_time | 12 | Time of bid request sent, YYYY-MM-DD HH:MM:SS in ET timezone | TIMESTAMP |  |
| buzz_key | 13 | Beeswax Buzz key, an identifier for client bidder instances | VARCHAR(255) |  |
| campaign_id | 14 | ID of the campaign that submitted the bid | INT4 |  |
| campaign_revenue_amount_micros | 15 | Amount of revenue set in the campaign config for completion of the   revenue type condition, in micros. 1 USD = 1,000,000 micros | INT8 |  |
| campaign_revenue_type | 16 | Campaign revenue type determines how revenue is booked by the advertiser   for a particular campaign; CPM or CPC (cost per click) basis | VARCHAR(255) |  |
| category | 17 | comma separate list of IAB-defined content categories:   http://www.iab.com/guidelines/iab-quality-assurance-guidelines-qag-taxonomy/;   determine type of content associated with a particular slice of inventory | VARCHAR(255) |  |
| clearing_price_micros_usd | 18 | Auction Clearing price(in micros) returned by exchange. This is the raw   media cost. 1 USD = 1,000,000 micros | INT8 |  |
| clicks | 19 | Set to 1 if the impression received a click | INT2 |  |
| content_coppa_flag | 20 | Children’s Online Privacy Protection Act (COPPA) Flag; inventory with   this flag carries several ad quality limitations | INT4 |  |
| content_language | 21 | Language in which content associated to the impression is written (as   declared by the publisher) | VARCHAR(255) |  |
| content_rating | 22 | Content parental rating (as declared by the publisher) | VARCHAR(255) |  |
| conversions | 23 | Number of conversions associated to a particular impression | INT4 |  |
| conversion_order | 24 | Conversion order, constitutes how many orders a particular conversion   represents; info provided by the advertiser in Beeswax UI/API | NUMERIC(18,6) |  |
| conversion_value | 25 | Value of a given conversion as ispecified by the advertiser in Beeswax   UI/API | NUMERIC(18,6) |  |
| create_time | 26 | Time created; Beeswax internal bookkeeping field | TIMESTAMP |  |
| creative_id | 27 | Beeswax ID for the creative that won an impression | INT4 |  |
| customer_id | 28 | Customer Beeswax ID | INT4 |  |
| deal_id | 29 | Populated with the impression's Deal ID if an impression was sold via a   deal. | VARCHAR(255) |  |
| domain | 30 | Domain name from which a given impression originated | VARCHAR(255) |  |
| environment_type | 31 | Environment type (APP or WEB) | VARCHAR(255) |  |
| exchange_discrepancy_rate_micros | 32 | Observed operational spend discrepancy between exchange and Beeswax. 1   micro = 0.000,0001% | INT8 |  |
| geo_city | 33 | City geo code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_country | 34 | Country geo name IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_metro | 35 | Metro geo code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_region | 36 | Geo region name IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_zip | 37 | Zip code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| has_frequency_cap | 38 | Frequency capped at campaign/lineitem level | INT2 |  |
| inventory_interstitial | 39 | determines if ad tag responsible for the impression accepts interstitial   creatives or not; 1 for yes, 0 for no | INT4 |  |
| inventory_source | 40 | Inventory source - exchange name | VARCHAR(255) |  |
| inventory_source_relationship | 41 | Inventory source relationship—direct or indirect | VARCHAR(255) |  |
| ip_address | 42 | IP address provided by the exchange during the auction. When no IPv4   address is present, the value is set to '0.0.0.0' | VARCHAR(255) |  |
| ip_range | 43 | IP address provided by the exchange during the auction (same as   ip_address) | VARCHAR(255) |  |
| line_item_id | 44 | Line Item ID that was responsible for winning the auction, as listed in   Beeswax | INT4 |  |
| line_item_revenue_amount_micros | 45 | Amount of revenue set in the line item config for completion of the   revenue type condition, in micros. 1 USD = 1,000,000 micros | INT8 |  |
| line_item_revenue_type | 46 | Type determines how the revenue was booked by the line item e.g. on a CPM   or CPC basis | VARCHAR(255) |  |
| placement | 47 | Placement ID/name, as provided by the publisher. Prefixed with exchange   handle. | VARCHAR(255) |  |
| platform_bandwidth | 48 | Shows whether the browser is using wifi or carrier to establish   connection with internet to generate the impression | VARCHAR(255) |  |
| platform_browser | 49 | Name of browser used during the auction for the impression at hand | VARCHAR(255) |  |
| platform_browser_version | 50 | Version of browser used to during the auction for the impression at hand | VARCHAR(255) |  |
| platform_carrier | 51 | If the device is using a mobile carrier to establish internet connection,   this field will identify which carrier is used | VARCHAR(255) |  |
| platform_device_didmd5 | 52 | Hardware device ID (e.g., IMEI); hashed via MD5 | VARCHAR(255) |  |
| platform_device_didsha1 | 53 | Hardware device ID (e.g., IMEI); hashed via SHA1 | VARCHAR(255) |  |
| platform_device_dpidmd5 | 54 | Platform device ID (e.g., Android ID); hashed via MD5 | VARCHAR(255) |  |
| platform_device_dpidsha1 | 55 | Platform device ID (e.g., Android ID); hashed via SHA1 | VARCHAR(255) |  |
| platform_device_idfa | 56 | iOS app ID; "Identifier for Advertisers"; deprecated | VARCHAR(255) |  |
| platform_device_ifa | 57 | ID sanctioned for advertiser use in the clear (i.e., not hashed) | VARCHAR(255) |  |
| platform_device_make | 58 | Make of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_model | 59 | Model of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_screen_size | 60 | Screensize of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_type | 61 | Type of the device used to generate the impression | VARCHAR(255) |  |
| platform_js | 62 | Indicates whether the browser supports JavaScript or not | INT4 |  |
| platform_os | 63 | Operating system of the device used to generate the impression | VARCHAR(255) |  |
| platform_os_version | 64 | Operating system version of the device used to generate the impression | VARCHAR(255) |  |
| pre_reduction_bid_price_micros_usd | 65 | Bid price returned by the bidding agent in micros. 1 USD = 1,000,000   micros | INT8 |  |
| revenue_amount_micros | 66 | Revenue in micros. Takes into account the Revenue Type to calculate   actual revenue generated by impression based on whether revenue condition was   achieved.This represents the actual revenue generated by an impression. 1 USD   = 1,000,000 micros | INT8 |  |
| segment_id | 67 | Beeswax segment ID; contains all segments the user qualifies for,   comma-delimited, regardless if it is targeted on the line item that won | VARCHAR(600) |  |
| segment_user_id | 68 | Beeswax segment user ID | INT2 |  |
| site_id | 69 | ID of the site that generated the impression, as provided by the   publisher | VARCHAR(255) |  |
| site_name | 70 | Name of the site that generated the impression, as provided by the   publisher | VARCHAR(255) |  |
| time_of_week | 71 | Time of week in GPS weekly time (minutes since Sunday midnight) of the   corresponding Bid Request in UTC. | INT4 |  |
| user_id | 72 | Primary user ID on the request. For web inventory: will populate with a   beeswax cookie ID if one is found, and fall back to device ID if not. For app   inventory: will populate with a device ID. | VARCHAR(255) |  |
| video_boxing_allowed | 73 | Indicates if letter-boxing of 4:3 content into a 16:9 window is allowed,   where 0 = no, 1 = yes | INT2 |  |
| video_companion_required | 74 | A banner companion ad is required to accompany the video ad: 0=false,   1=true | INT4 |  |
| video_completes | 75 | Number of videos watched through completion; Set to 1 if video watched   through completion | INT2 |  |
| video_midpoints | 76 | Number of videos watched through video midpoint; Set to 1 if video   watched through video midpoint | INT2 |  |
| video_playback_method | 77 | Video playback method, as determined by the publisher. | VARCHAR(255) |  |
| video_player_size | 78 | Video player size | VARCHAR(255) |  |
| video_plays | 79 | Number of video plays; Set to 1 if video plays | INT2 |  |
| video_q1s | 80 | Number of videos watched the first quarter; Set to 1 if video watched   through the first quarter | INT2 |  |
| video_q3s | 81 | Number of videos watched through the third quarter; Set to 1 if video   watched through the third quarter | INT2 |  |
| video_skips | 82 | Number of video skips; Set to 1 if video is skipped | INT2 |  |
| video_start_delay | 83 | Indicates the start delay in seconds for pre-roll, mid-roll, or post-roll   video ad placements. | INT2 |  |
| win_cost_micros_usd | 84 | 1 USD = 1,000,000 micros. Media Spend + Vendor Fees in USD$ (when 'Spend with Vendor Fees' is selected as the 'Budget Type' on the Line Item. If 'Spend' is selected, this will equal 'Media Spend') | INT8 |  |
| advertiser_id | 85 | Advertiser ID for the impression | INT8 |  |
| vendor_fee_micros_usd | 86 | Vendor fee in micros, USD 1 USD = 1,000,000 micros | INT8 |  |
| test | 87 | Indicator of test mode in which auctions are not billable, where t = live   mode, f = test mode | BOOLEAN |  |
| placement_type | 88 | Placement type, indicates whether the placement is meant for banner,   video ads, or both | VARCHAR(255) |  |
| geo_lat | 89 | Latitude associated with the impression | VARCHAR(50) |  |
| geo_lon | 90 | Longitude associated with the impression | VARCHAR(50) |  |
| total_cpm_vendor_fee_amount_micros | 91 | Internal, tracks total vendor fee per CPM. 1 USD = 1,000,000 micros | INT8 |  |
| total_percent_vendor_fee_amount_micros | 92 | Internal, tracks total vendor fee percentage of win_cost_micros_usd. 1   USD = 1,000,000 micros | INT8 |  |
| bid_time_epoch_in_usecs | 93 | bid timestamp(epoch) with microsecond precision. Allows the customer to   calculate the bid_time in any timezone instead of relying on `bid_time` field   which is ET timezone | INT8 |  |
| model_id | 94 | Holds the `agent_id` field value of the BidAgentResponse returned by the   customer's bidding agent. If the line item uses Bid Models and the Bid Model   matches the incoming bid request, this field will contain the Bid Model ID.   This can be used for debugging. | VARCHAR(255) |  |
| model_params | 95 | Holds the `agent_params` field value of the BidAgentResponse return by   the customer's bidding agent. If the line item uses Bid Models, this will   contain the cache results for the Bid Model lookup. This can be used for   debugging. Format => {key}={value},{key}={value}.. | VARCHAR(600) |  |
| data_center | 96 | Beeswax's data center responsible for processing the bid request/response   in question | VARCHAR(50) |  |
| billing_version | 97 | Internal | VARCHAR(50) |  |
| in_view | 98 | Determines if the impression is viewable or not | INT2 |  |
| is_measurable | 99 | Determines if the impression is measurable for viewability or not | INT2 |  |
| in_view_time_millis | 100 | States how much time the impression was in view, measured in miliseconds | INT8 |  |
| bidding_strategy_id | 101 | ID of the custom bidding strategy in Beeswax | VARCHAR(255) |  |
| bidding_strategy_params | 102 | Parameters passed along by the client for the custom bidding strategy in   Beeswax | VARCHAR(255) |  |
| exchange_predicted_view_rate | 103 | Estimated viewability rate, provided by the auction host | NUMERIC(18,6) |  |
| rx_timestamp | 104 | Impression Event received time in ET timezone | TIMESTAMP |  |
| battrs | 105 | Creative attributes that are blocked by the publisher, as declared by the   publisher | VARCHAR(255) |  |
| exchange_auction_id | 106 | Auction ID generated by the auction host ; different to that of Beeswax | VARCHAR(255) |  |
| rewarded | 107 | States whether the placement tag behind the impression is meant for   rewarded ads | INT2 |  |
| currency_rate | 108 | Currency exchange rate (in decimal) at the auction time | NUMERIC(18,10) |  |
| currency_code | 109 | Three letter currency codes setup in buzz | VARCHAR(10) |  |
| clearing_price_micros | 110 | Auction Clearing price(in micros) returned by exchange. This is the raw   media cost 1 Unit of Line Item's set Currency = 1,000,000 micros | INT8 |  |
| win_cost_micros | 111 | 1 Unit of Line Item's set Currency =   1,000,000 micros. Media Spend + Vendor Fees in USD$ (when 'Spend with Vendor Fees' is selected as the 'Budget Type' on the Line Item. If 'Spend' is selected, this will equal 'Media Spend')| INT8 |  |
| bid_price_micros | 112 | Bid price sent to the exchange (in micros, post-reduction). 1   Unit of Line Item's set Currency = 1,000,000 micros | INT8 |  |
| vendor_fee_micros | 113 | Vendor fee in micros. 1 Unit of Vendor Fee's set Currency = 1,000,000   micros | INT8 |  |
| viewability_vendor_name | 114 | Vendor used for providing viewability metrics | VARCHAR(10) |  |
| conversion_update_time | 115 | Formerly used internally | TIMESTAMP |  |
| companion_clicks | 116 | Set to 1 if the video's companion banner received a click | INT2 |  |
| companion_views | 117 | Set to 1 if the video's companion banner served an impression | INT2 |  |
| banner_width | 118 | Width of the impression in pixels | INT4 |  |
| banner_height | 119 | Height of the impression in pixels | INT4 |  |
| bid_floor_micros | 120 | The floor or lowest allowable clearing price of the auction. 1 USD =   1,000,000 micros | INT8 |  |
| bid_floor_currency | 121 | If the bid floor is specified and multiple currencies are supported per   bid request, the currency of the bid floor using ISO-4217 codes | VARCHAR(10) |  |
| display_manager | 122 | Name of the ad mediation partner, SDK technology, or player responsible   for rendering ad (typically video or mobile). Used by some ad servers to   customize ad code by partner. | VARCHAR(255) |  |
| display_manager_ver | 123 | Version of display_manager | VARCHAR(255) |  |
| exchange_device_make | 124 | Device make provided by the exchange, e.g. "Apple" | VARCHAR(255) |  |
| exchange_device_model | 125 | Device model provided by the exchange, e.g. "iPhone" | VARCHAR(255) |  |
| line_item_alt_id | 126 | Alternative ID in Buzz of the Line Item | VARCHAR(255) |  |
| page_url | 127 | URL of the page responsible for the auction | VARCHAR(255) |  |
| auction_type | 128 | If 1, first price auction. If 2, second price auction. Additional auction   types can be defined as per the exchange's business rules | INT4 |  |
| publisher_id | 129 | Publisher ID on the exchange. Prefixed with the exchange handle for   uniqueness | VARCHAR(255) |  |
| ads_txt | 130 | Ads.txt status for the request. It is an enum field, and can be one of   the following values: UNKNOWN - The request was not augmented by the ads.txt   augmentor (should never happen) NO_DOMAIN - The request does not contain a   domain, either because it is not a web request (ie it is an app or native   request) or it is a web request but does not contain a domain NO_ADS_TXT_FILE   - The request's domain does not have an Ads.txt file ADS_TXT_NOT_SCANNED - We   have not looked up the Ads.txt file for the request's domain   NO_ADVERTISING_ALLOWED - The request's domain does not allow any advertising   MISSING_PUB_ID - The request is missing a publisher id so we cannot check its   Ads.txt status NOT_AUTH - The request's domain does have an Ads.txt file, but   it does not allow advertising from this exchange / publisher ID combination   AUTH_RESELLER - The domain's Ads.txt file allows this exchange / publisher ID   to resell advertising AUTH_DIRECT - The domain's Ads.txt file allows this   exchange / publisher ID to advertise directly | VARCHAR(20) |  |
| bid_modifier_id | 131 | ID of the Bid Modifier in Buzz | INT8 |  |
| bid_modifier_multipliers_product | 132 | Combined bid modifier multiplier applied to the bid | NUMERIC(18.6) |  |
| matched_user_groups | 133 | Matched user IDs for match tables hosted by Beeswax | VARCHAR(255) |  |
| ipv6_address | 134 | IPv6 address provided by the exchange during the auction. When no IPv6   address is present, the value is set to '0:0:0:0:0:0:0:0' | VARCHAR(255) |  |
| flight_id | 135 | ID of the Line Item Flight in Buzz (if present) | INT4 |  |
| user_id_hashed | 136 | GDPR-compliant hashed user_id | VARCHAR(255) |  |
| ip_address_hashed | 137 | GDPR-compliant hashed ip | VARCHAR(255) |  |
| ipv6_address_hashed | 138 | GDPR-compliant hashed ipv6 | VARCHAR(255) |  |
| is_gdpr | 139 | When this field is set to true, Beeswax has determined that this request   needs to comply with GDPR | INT2 |  |
| gdpr_consent_string | 140 | The raw IAB GDPR consent string as provided in the bid request | VARCHAR(255) |  |
| targeted_segments | 141 | Beeswax segment ID; contains all segments the user qualifies for that   were also targeted on the line item that won | VARCHAR(600) |  |
| clicks_ip_address | 142 | Comma delimited list of all unique IP adresses of all clicks (regular and   companion) associated with this impression | VARCHAR(255) |  |
| request_id | 143 | Unique ID for every bid request in the system. A joining key for all the   events associated with the bid request, like impression, clicks, and   activities. Note that it is possible to have multiple auction_ids for a   single request_id | VARCHAR(255) |  |
| person_linked_ids | 144 | Deprecated; will not be populated. | VARCHAR(600) |  |
| household_linked_ids | 145 | Deprecated; will not be populated. | VARCHAR(600) |  |
| video_protocols | 146 | Comma-separated list of video protocols that are accepted by the   publisher | VARCHAR(255) |  |
| clicks_user_id | 147 | The user ID captured on the click event | VARCHAR(255) |  |
| clicks_user_id_hashed | 148 | The user ID (hashed) captured on the click event | VARCHAR(255) |  |
| user_time_of_week | 149 | Time of week in GPS weekly time (minutes since Sunday midnight) of the   corresponding Bid Request in the user's local timezone. | INT4 |  |
| bot_clicks | 150 | Set to 1 if a click is suspected to originate from bot traffic | INT2 |  |
| bid_time_utc | 151 | Time of bid request sent, in UTC timezone | TIMESTAMP |  |
| rx_timestamp_utc | 152 | Time of receipt of the Impression Event, in UTC timezone | TIMESTAMP |  |
| test_group_id | 153 | ID of the Test Group the user fell into within the test plan. Should   match the Test Group assigned to the line item | INT4 |  |
| experiment_user_index | 154 | Random number between 1-1000 assigned to a user. Used for test group   assignment | INT4 |  |
| test_plan_id | 155 | ID of the Test Plan associated with the campaign | INT4 |  |
| inventory_source_user_id | 156 | Unique consumer ID of the user, as defined by the exchange. | VARCHAR(255) |  |
| mccmnc | 157 | Mobile carrier as defined by the concatenated MCC-MNC code. | VARCHAR(255) |  |
| us_privacy | 158 | US Privacy String as defined by the IAB CCPA Compliance Framework, and   used to define the regulatory context governing the personal data contained   within the associated bid request. | VARCHAR(255) |  |
| geo_type | 159 | LocationType, how the geographic information was determined | VARCHAR(20) |  |
| video_placement | 160 | The placement of the video impression (e.g., In-Stream) | VARCHAR(255) |  |
| publisher_name | 161 | Publisher Name as specified on the OpenRTB request. | VARCHAR(255) |  |
| freq_cap_id_type | 162 | Comma-separated list of the ID types that were used to perform frequency   capping for the impression | VARCHAR(255) |  |
| campaign_alt_id | 163 | Alternative ID in Buzz of the Campaign | VARCHAR(255) |  |
| exchange_imp_id | 164 | The ID of the Impression that was won. Relevant for multi-impression   auctions. Derived from OpenRTB's Impression ID object. | VARCHAR(255) |  |
| ua | 165 | The Useragent of the impression | VARCHAR(255) |  |
| seller_id | 166 | The value of the corresponding seller in sellers.json files. Only   populated when the exchange uses a different value for this than in Publisher   ID. | VARCHAR(255) |  |
| deal_bid_floors | 167 | Bid floor of the winning deal ID | VARCHAR(255) |  |
| site_referrer | 168 | The referrer to the site the auction occurred on. | VARCHAR(255) |  |
| bid_shade | 169 | The Bid Shade Status of the won impression. Will be one of: NOT_ELIGIBLE   - Line Item was ineligible for bid shading BID_SHADED - Line Item had its bid   shaded. CONTROL_GROUP - Line Item was eligible for bid shading but was   selected for the control group of the algorithm. | VARCHAR(255) |  |
| bid_shade_reduction_micros | 170 | Value the bid was shaded by in micros. | INT8 |  |
| video_mutes | 171 | Count of Video muted events. | INT8 |  |
| video_unmutes | 172 | Count of Video unmuted events. | INT8 |  |
| video_pauses | 173 | Count of Video pause events. | INT8 |  |
| video_resumes | 174 | Count of Video resume events. | INT8 |  |
| video_fullscreens | 175 | Count of Video fullscreen events. | INT8 |  |
| video_closes | 176 | Count of Video close events. | INT8 |  |
| impression_ip_address | 177 | The IP address of the impression; contrasted to ip_address, which derives   its IP from the bid request. | VARCHAR(255) |  |
| video_api | 178 | List of supported API frameworks for this impression. | VARCHAR(255) |  |
| bid_shading_fee_type | 179 | The Bid Shading Fee Type for the Impression. Will be one of: N/A: No bid   shading was used on the impression. VENDOR_FEE: The impression was using a   CUSTOMER_BILLABLE seat and the bid shading fee will be charged as a vendor   fee. INCLUDED_IN_WIN_PRICE: The impression was using a BEESWAX_BILLABLE seat   and the bid shading fee will be added to the media spend. | VARCHAR(255) |  |
| bid_shading_fee_micros_usd | 180 | The bid shading fee charged for the impression expressed in micros, in   USD. 1 USD = 1,000,000 micros | INT8 |  |
| bid_shading_fee_micros | 181 | The bid shading fee charged for the impression expressed in micros, in   local currency of the line item. 1 Unit of Currency = 1,000,000 micros | INT8 |  |
| require_native_video | 182 | If the creative for the impression is of type Native, this field will be   set to 1 when a video asset is required. The field will be 0 in all other   cases. | INT2 |  |
| is_gdpr_consented | 183 | Whether the auction is regulated by GDPR AND the customer has been   granted consent by the end user. | INT2 |  |
| targeted_lat_long_lists | 184 | The names of the lat/long lists specified that were targeted and matched   on the given request. | VARCHAR(255) |  |
| qag_media_rating | 185 | If defined, contains the QAG Media Rating of the content as defined by   OpenRTB spec. | VARCHAR(255) |  |
| media_spend_micros | 186 | The total cost of media for the impression expressed in micros in the the   local currency of the line item. 1 Unit of Currency = 1,000,000 micros | INT8 |  |
| media_spend_micros_usd | 187 | The total cost of media for the impression expressed in micros in US   dollars. 1 Unit of Currency = 1,000,000 micros | INT8 |  |
| guaranteed | 188 | Indicates whether a given line item is a guaranteed line item or not. | INT2 |  |
| creative_alt_id | 189 | If set, the alternative ID of the creative that won the auction will   populate in this column. | VARCHAR(255) |  |
| creative_name | 190 | The name of the creative as specified in Buzz. | VARCHAR(255) |  |
| lat_long_list_item_ids | 191 | Comma-separated list of unique keys describing the matching lat/long list   item IDs for this event. Formed as the cocatenation of the List ID and List   Item ID separated by a colon (:). e.g. buzz_key-10:9292 | VARCHAR(255) |  |
| lat_long_list_item_names | 192 | Comma-separated list of names (if set) for the the matching lat/long list   item IDs for this event. Displayed in the same order as the IDs in the   previous column. If no name is set for the matched list item then the field   will be set to an empty string for each given list item id. If multiple list   items match this field may have multiple commas with no values in it. | VARCHAR(255) |  |
| click_rx_timestamp_utc | 193 | If a click was joinable to this impression, this column contains the   timestamp of receipt of the event. | TIMESTAMP |  |
| bcat | 194 | Blocked advertiser categories using the IAB content categories. | VARCHAR(255) |  |
| platform_device_hwv | 195 | The hardware version as specified in the OpenRTB specification | VARCHAR(255) |  |
| platform_device_language | 196 | Browser language using ISO-639-1-alpha-2 as specified in the OpenRTB   specification | VARCHAR(255) |  |
| platform_device_w | 197 | The physical device's width in pixels as specified in the OpenRTB   specification | INT4 |  |
| platform_device_h | 198 | The physical device's height in pixels as specified in the OpenRTB   specification | INT4 |  |
| platform_device_ppi | 199 | The device's screen size as express in pixels per inch, as specified in   OpenRTB specification | INT4 |  |
| platform_device_pxratio | 200 | The ratio of physical pixels to device independent pixels, as specified   in OpenRTB specification | NUMERIC(18,6) |  |
| invalid_impression | 201 | Specifies whether an impression may be viewed as IVT contingent on vendor   rules. | INT2 |  |
| is_invalid_measurable | 202 | Specifies whether an impression was measurable for IVT tracking purposes. | INT2 |  |
| invalid_automated_browser | 203 | Flags whether an IVT impression was viewed as originating from an   automated browser. | INT2 |  |
| invalid_incongruous_browser | 204 | Flags whether an IVT impression was viewed as originating from an   incongruous browser. | INT2 |  |
| invalid_data_center_traffic | 205 | Flags whether an IVT impression was viewed as originating from a data   center. | INT2 |  |
| invalid_impression_vendor_name | 206 | The name of the vendor from which IVT fields were populated. | VARCHAR(10) |  |
| experiment_id_type | 207 | The ID type used for segregation of impressions for Beeswax's experiment   feature. | VARCHAR(255) |  |
| deal_auction_type | 208 | If the impression was purchased via a deal, this logs the auction type   for the deal. 1 = First Price, 2 = Second Price, 3 = Fixed Price. Overrides   "auction_type |  |  |
| account_level_revenue_share_fee_type | 209 | If using the account-level revenue share feature, this column populates   whether the fee is expressed as a reduction or fee. | VARCHAR(255) |  |
| account_level_revenue_share_percent_micros | 210 | If using the account-level revenue share feature, this column populates   the percentage of the rev share for the given impression in micros. | INT8 |  |
| account_level_revenue_share_micros_usd | 211 | As above, but populates the calcualted value of the rev share in USD as   expressed in micros. | INT8 |  |
| account_level_revenue_share_micros | 212 | As above, but populates the calcualted value of the rev share in the   local currency as expressed in micros. | INT8 |  |
| tmax | 213 | The required time in milliseconds for the bid to respond to the exchange   to be considered in the auction | INT4 |  |
| video_skippable | 214 | If the ad is a video ad, this field indicates whether the creative   trafficked could have been skippable. | INT2 |  |
| is_skadnetwork | 215 | Flags whether the inventory is SKAdNetwork enabled. | INT2 |  |
| dnt | 216 | Do Not Track | INT4 |  |
| lmt | 217 | Limit Ad Tracking (LMT) is a device-level opt-out setting, that allows   users to limit the amount of information sent from their device to ad   exchanges (including omitting their device ID) | INT2 |  |
| banner_format | 218 | Comma-separated list of banner formats (wxh) that are accepted by the   publisher | VARCHAR(255) |  |
| content_id | 219 | ID uniquely identifying the content | VARCHAR(255) |  |
| content_episode | 220 | Episode number | VARCHAR(255) |  |
| content_title | 221 | Content title | VARCHAR(255) |  |
| content_series | 222 | Content series | VARCHAR(255) |  |
| content_season | 223 | Content season | VARCHAR(255) |  |
| content_genre | 224 | Genre that best describes the content | VARCHAR(255) |  |
| content_contentrating | 225 | Content rating (e.g., MPAA) | VARCHAR(255) |  |
| content_keywords | 226 | Comma separated list of keywords describing the content | VARCHAR(255) |  |
| content_livestream | 227 | 0 = not live, 1 = content is live (e.g., stream, live blog) | INT4 |  |
| content_len | 228 | Length of content in seconds; appropriate for video or audio | VARCHAR(255) |  |
| content_network_id | 229 | ID of the network the content is on. This may not be a unique identifier   across all supply sources | VARCHAR(255) |  |
| content_network_name | 230 | Network the content is on (e.g., a TV network like “ABC") | VARCHAR(255) |  |
| content_network_domain | 231 | The primary domain of the network (e.g. “abc.com” in the case of the   network ABC). | VARCHAR(255) |  |
| content_channel_id | 232 | ID of the channel the content is on. This may not be a unique identifier   across all supply sources | VARCHAR(255) |  |
| content_channel_name | 233 | Channel the content is on (e.g., a local channel like “WABC-TV") | VARCHAR(255) |  |
| content_channel_domain | 234 | The primary domain of the channel (e.g. “abc7ny.com” in the case of the   local channel WABC-TV) | VARCHAR(255) |  |
| content_cat | 235 | Array of IAB content categories that describe the content | VARCHAR(255) |  |
| ip_conversions | 236 | Number of IP conversions associated to a particular impression | INT4 |  |
| ip_conversion_order | 237 | IP conversion order, constitutes how many orders a particular IP   conversion represents; info provided by the advertiser in Beeswax UI/API | NUMERIC(18,6) |  |
| ip_conversion_value | 238 | Value of a given IP conversion as ispecified by the advertiser in Beeswax   UI/API | NUMERIC(18,6) |  |
| master_revenue_share_percent_micros | 239 | If using a master revenue share, a micro value percentage represent the   revenue share being taken. | INT8 |  |
| master_revenue_share_micros_usd | 240 | Master revenue share amount in USD. | INT8 |  |
| master_revenue_share_micros | 241 | Master revenue share amount in bid currency. | INT8 |  |
| total_vendor_fees_micros_usd | 242 | Total fee amount withheld in USD, inclusive of master revenue share. | INT8 |  |
| total_vendor_fees_micros | 243 | Total fee amount withheld in bid currency, inclusive of master revenue   share. | INT8 |  |
| delivery_modifier_id | 244 | The ID of the Delivery Modifier. | INT4 |  |
| delivery_model_id | 245 | The ID of the Delivery Model. | VARCHAR(255) |  |
| bid_model_id | 246 | The ID of the Bid Model, formatted like   {buzz_key}-{bid_model_id}-(bid_model_version}. | VARCHAR(255) |  |
| bid_model_params | 247 | The cache results for the Bid Model lookup, formatted like   {key}={value},{key}={value} | VARCHAR(600) |  |
| bid_agent_id | 248 | Holds the agent_id field value of the BidAgentResponse returned by the   customer's bidding agent. | VARCHAR(255) |  |
| bid_agent_params | 249 | Holds the agent_params field value of the BidAgentResponse return by the   customer's bidding agent. | VARCHAR(600) |  |
| topics_id | 250 | Represents the Topics ID from the taxonomy identified by the Taxonomy   Version. | VARCHAR(255) |  |
| topics_taxonomy_version | 251 | The ID associated with a taxonomy that is registered centrally with the   IAB Tech Lab in Enumeration of Taxonomies. | VARCHAR(255) |  |
| audio_plays | 252 | Set to 1 if audio ad is played. | INT4 |  |
| audio_q1s | 253 | Set to 1 if audio ad is watched through the first quartile. | INT4 |  |
| audio_midpoints | 254 | Set to 1 if audio ad is watched through the second quartile. | INT4 |  |
| audio_q3s | 255 | Set to 1 if audio ad is watched through the third quartile. | INT4 |  |
| audio_completes | 256 | Set to 1 if audio ad is watched through the fourth quartile. | INT4 |  |
| audio_skips | 257 | Set to 1 if audio ad is skipped. | INT4 |  |
| bw_content_genre | 258 | The mapped Beeswax Content Genre from the taxonomy. This field will only   be populated for video bid requests. | VARCHAR(255) |  |
| audio_startdelay | 259 | Indicates the start delay in seconds for pre-roll, mid-roll, or post-roll   audio ad placements. | INT4 |  |
| audio_minbitrate | 260 | The minimum allowed bitrate, in Kbps. | INT4 |  |
| audio_maxbitrate | 261 | The maximum allowed bitrate, in Kbps. | INT4 |  |
| audio_feed | 262 | The type of feed for audio requests. | VARCHAR(50) |  |
| audio_companion_required | 263 | A banner companion ad is required to accompany the audio ad: 0=false, 1=true, -1=unknown, not provided, null, etc. | INT4 |  |
| bidreq_universal_ids | 264 | Comma-separated list of encrypted ID5 universal ID values | VARCHAR(255) |  |
| video_plcmt | 265 | The placement of the video impression. 1=INSTREAM, 2=ACCOMPANYING CONTENT, 3=INTERSTITIAL, 4=NO CONTENT/STANDALONE | VARCHAR(255) |  |
| app_ads_txt | 266 | App Ads.txt status for the request. It is an enum field, and can be one of the following values: Unauthorized, Authorized - Direct, Authorized - Reseller, Unknown, Authorized  | VARCHAR(50) |  |
