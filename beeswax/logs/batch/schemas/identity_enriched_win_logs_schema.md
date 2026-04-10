| Header | Position | Definition | SQL_Datatype | DDL Description |
|---|---|---|---|---|
| enriched_person_ids | 1 | Person-level enriched IDs in the customer-configured identity namespace that the FreeWheel Identity Network has linked to this impression. Contains all matched person-level IDs for the selected enrichment ID type, or is empty when no eligible matches are found. | VARCHAR | |
| enriched_household_ids | 2 | Household-level enriched IDs in the customer-configured identity namespace that the FreeWheel Identity Network has linked to this impression. Contains all household-level matches the FreeWheel Identity Network has linked to this impression for the selected enrichment type, or is empty when no eligible matches are found. | VARCHAR | |
|account_id | 3 | Beeswax bidder account ID; represents the bidder seat for a particular   client | INT4 |  |
| ad_position | 4 | If applicable, ad position on page | VARCHAR(255) |  |
| app_bundle | 5 | Application bundle or package name (e.g., com.foo.mygame). This is   intended to be a unique ID across multiple exchanges. | VARCHAR(255) |  |
| app_id | 6 | Application ID on the exchange. For uniqueness, Uses ad exchange/SSP   identifier as prefix e.g. pm/ representing pubmatic | VARCHAR(255) |  |
| app_name | 7 | Application name | VARCHAR(255) |  |
| auction_adgroup_id | 8 | Internal Unique ID | VARCHAR(255) |  |
| auction_id | 9 | Unique ID for every bid request in the system. A joining key for all the   events associated with the bid request, like impression, clicks, and   activities. | VARCHAR(255) |  |
| beeswax_fee_rate_micros | 10 | For PERCENT fee-type option, applicable Beeswax fee rate in micros 1   micro = 0.000,0001% | INT8 |  |
| bid_hour | 11 | Datestamp during which a particular bid was made, YYYY-MM-DD HH:00:00 in   ET timezone | TIMESTAMP |  |
| bid_price_micros_usd | 12 | Bid price returned by the bidding agent (in USD micros) after bid shading is applied. 1 USD = 1,000,000 micros | INT8 |  |
| bid_reduction_rate_micros | 13 | For BID_REDUCTION(rev-share) fee type option, applicable Bid reduction   rate in micros 1 micro = 0.000,0001% | INT8 |  |
| bid_time | 14 | Time of bid request sent, YYYY-MM-DD HH:MM:SS in ET timezone | TIMESTAMP |  |
| buzz_key | 15 | Beeswax Buzz key, an identifier for client bidder instances | VARCHAR(255) |  |
| campaign_id | 16 | ID of the campaign that submitted the bid | INT4 |  |
| campaign_revenue_amount_micros | 17 | Amount of revenue set in the campaign config for completion of the   revenue type condition, in micros. 1 USD = 1,000,000 micros | INT8 |  |
| campaign_revenue_type | 18 | Campaign revenue type determines how revenue is booked by the advertiser   for a particular campaign; CPM or CPC (cost per click) basis | VARCHAR(255) |  |
| category | 19 | comma separate list of IAB-defined content categories:   http://www.iab.com/guidelines/iab-quality-assurance-guidelines-qag-taxonomy/;   determine type of content associated with a particular slice of inventory | VARCHAR(255) |  |
| clearing_price_micros_usd | 20 | Auction Clearing price(in micros) returned by exchange. This is the raw   media cost. 1 USD = 1,000,000 micros | INT8 |  |
| clicks | 21 | Set to 1 if the impression received a click | INT2 |  |
| content_coppa_flag | 22 | Children’s Online Privacy Protection Act (COPPA) Flag; inventory with   this flag carries several ad quality limitations | INT4 |  |
| content_language | 23 | Language in which content associated to the impression is written (as   declared by the publisher) | VARCHAR(255) |  |
| content_rating | 24 | Content parental rating (as declared by the publisher) | VARCHAR(255) |  |
| conversions | 25 | Number of conversions associated to a particular impression | INT4 |  |
| conversion_order | 26 | Conversion order, constitutes how many orders a particular conversion   represents; info provided by the advertiser in Beeswax UI/API | NUMERIC(18,6) |  |
| conversion_value | 27 | Value of a given conversion as ispecified by the advertiser in Beeswax   UI/API | NUMERIC(18,6) |  |
| create_time | 28 | Time created; Beeswax internal bookkeeping field | TIMESTAMP |  |
| creative_id | 29 | Beeswax ID for the creative that won an impression | INT4 |  |
| customer_id | 30 | Customer Beeswax ID | INT4 |  |
| deal_id | 31 | Populated with the impression's Deal ID if an impression was sold via a   deal. | VARCHAR(255) |  |
| domain | 32 | Domain name from which a given impression originated | VARCHAR(255) |  |
| environment_type | 33 | Environment type (APP or WEB) | VARCHAR(255) |  |
| exchange_discrepancy_rate_micros | 34 | Observed operational spend discrepancy between exchange and Beeswax. 1   micro = 0.000,0001% | INT8 |  |
| geo_city | 35 | City geo code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_country | 36 | Country geo name IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_metro | 37 | Metro geo code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_region | 38 | Geo region name IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_zip | 39 | Zip code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| has_frequency_cap | 40 | Frequency capped at campaign/lineitem level | INT2 |  |
| inventory_interstitial | 41 | determines if ad tag responsible for the impression accepts interstitial   creatives or not; 1 for yes, 0 for no | INT4 |  |
| inventory_source | 42 | Inventory source - exchange name | VARCHAR(255) |  |
| inventory_source_relationship | 43 | Inventory source relationship—direct or indirect | VARCHAR(255) |  |
| ip_address | 44 | IP address provided by the exchange during the auction. When no IPv4   address is present, the value is set to '0.0.0.0' | VARCHAR(255) |  |
| ip_range | 45 | IP address provided by the exchange during the auction (same as   ip_address) | VARCHAR(255) |  |
| line_item_id | 46 | Line Item ID that was responsible for winning the auction, as listed in   Beeswax | INT4 |  |
| line_item_revenue_amount_micros | 47 | Amount of revenue set in the line item config for completion of the   revenue type condition, in micros. 1 USD = 1,000,000 micros | INT8 |  |
| line_item_revenue_type | 48 | Type determines how the revenue was booked by the line item e.g. on a CPM   or CPC basis | VARCHAR(255) |  |
| placement | 49 | Placement ID/name, as provided by the publisher. Prefixed with exchange   handle. | VARCHAR(255) |  |
| platform_bandwidth | 50 | Shows whether the browser is using wifi or carrier to establish   connection with internet to generate the impression | VARCHAR(255) |  |
| platform_browser | 51 | Name of browser used during the auction for the impression at hand | VARCHAR(255) |  |
| platform_browser_version | 52 | Version of browser used to during the auction for the impression at hand | VARCHAR(255) |  |
| platform_carrier | 53 | If the device is using a mobile carrier to establish internet connection,   this field will identify which carrier is used | VARCHAR(255) |  |
| platform_device_didmd5 | 54 | Hardware device ID (e.g., IMEI); hashed via MD5 | VARCHAR(255) |  |
| platform_device_didsha1 | 55 | Hardware device ID (e.g., IMEI); hashed via SHA1 | VARCHAR(255) |  |
| platform_device_dpidmd5 | 56 | Platform device ID (e.g., Android ID); hashed via MD5 | VARCHAR(255) |  |
| platform_device_dpidsha1 | 57 | Platform device ID (e.g., Android ID); hashed via SHA1 | VARCHAR(255) |  |
| platform_device_idfa | 58 | iOS app ID; "Identifier for Advertisers"; deprecated | VARCHAR(255) |  |
| platform_device_ifa | 59 | ID sanctioned for advertiser use in the clear (i.e., not hashed) | VARCHAR(255) |  |
| platform_device_make | 60 | Make of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_model | 61 | Model of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_screen_size | 62 | Screensize of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_type | 63 | Type of the device used to generate the impression | VARCHAR(255) |  |
| platform_js | 64 | Indicates whether the browser supports JavaScript or not | INT4 |  |
| platform_os | 65 | Operating system of the device used to generate the impression | VARCHAR(255) |  |
| platform_os_version | 66 | Operating system version of the device used to generate the impression | VARCHAR(255) |  |
| pre_reduction_bid_price_micros_usd | 67 | Bid price returned by the bidding agent in micros. 1 USD = 1,000,000   micros | INT8 |  |
| revenue_amount_micros | 68 | Revenue in micros. Takes into account the Revenue Type to calculate   actual revenue generated by impression based on whether revenue condition was   achieved.This represents the actual revenue generated by an impression. 1 USD   = 1,000,000 micros | INT8 |  |
| segment_id | 69 | Beeswax segment ID; contains all segments the user qualifies for,   comma-delimited, regardless if it is targeted on the line item that won | VARCHAR(600) |  |
| segment_user_id | 70 | DEPRECATED. Beeswax segment user ID | INT2 |  |
| site_id | 71 | ID of the site that generated the impression, as provided by the   publisher | VARCHAR(255) |  |
| site_name | 72 | Name of the site that generated the impression, as provided by the   publisher | VARCHAR(255) |  |
| time_of_week | 73 | Time of week in GPS weekly time (minutes since Sunday midnight) of the   corresponding Bid Request in UTC. | INT4 |  |
| user_id | 74 | Primary user ID on the request. For web inventory: will populate with a   beeswax cookie ID if one is found, and fall back to device ID if not. For app   inventory: will populate with a device ID. | VARCHAR(255) |  |
| video_boxing_allowed | 75 | Indicates if letter-boxing of 4:3 content into a 16:9 window is allowed,   where 0 = no, 1 = yes | INT2 |  |
| video_companion_required | 76 | A banner companion ad is required to accompany the video ad: 0=false,   1=true | INT4 |  |
| video_completes | 77 | Number of videos watched through completion; Set to 1 if video watched   through completion | INT2 |  |
| video_midpoints | 78 | Number of videos watched through video midpoint; Set to 1 if video   watched through video midpoint | INT2 |  |
| video_playback_method | 79 | Video playback method, as determined by the publisher. | VARCHAR(255) |  |
| video_player_size | 80 | Video player size | VARCHAR(255) |  |
| video_plays | 81 | Number of video plays; Set to 1 if video plays | INT2 |  |
| video_q1s | 82 | Number of videos watched the first quarter; Set to 1 if video watched   through the first quarter | INT2 |  |
| video_q3s | 83 | Number of videos watched through the third quarter; Set to 1 if video   watched through the third quarter | INT2 |  |
| video_skips | 84 | Number of video skips; Set to 1 if video is skipped | INT2 |  |
| video_start_delay | 85 | Indicates the start delay in seconds for pre-roll, mid-roll, or post-roll   video ad placements. | INT2 |  |
| win_cost_micros_usd | 86 | 1 USD = 1,000,000 micros. Media Spend + Vendor Fees in USD$ (when 'Spend with Vendor Fees' is selected as the 'Budget Type' on the Line Item. If 'Spend' is selected, this will equal 'Media Spend') | INT8 |  |
| advertiser_id | 87 | Advertiser ID for the impression | INT8 |  |
| vendor_fee_micros_usd | 88 | Vendor fee in micros, USD 1 USD = 1,000,000 micros | INT8 |  |
| test | 89 | Indicator of test mode in which auctions are not billable, where t = live   mode, f = test mode | BOOLEAN |  |
| placement_type | 90 | Placement type, indicates whether the placement is meant for banner,   video ads, or both | VARCHAR(255) |  |
| geo_lat | 91 | Latitude associated with the impression | VARCHAR(50) |  |
| geo_lon | 92 | Longitude associated with the impression | VARCHAR(50) |  |
| total_cpm_vendor_fee_amount_micros | 93 | Internal, tracks total vendor fee per CPM. 1 USD = 1,000,000 micros | INT8 |  |
| total_percent_vendor_fee_amount_micros | 94 | Internal, tracks total vendor fee percentage of win_cost_micros_usd. 1   USD = 1,000,000 micros | INT8 |  |
| bid_time_epoch_in_usecs | 95 | bid timestamp(epoch) with microsecond precision. Allows the customer to   calculate the bid_time in any timezone instead of relying on `bid_time` field   which is ET timezone | INT8 |  |
| model_id | 96 | Holds the `agent_id` field value of the BidAgentResponse returned by the   customer's bidding agent. If the line item uses Bid Models and the Bid Model   matches the incoming bid request, this field will contain the Bid Model ID.   This can be used for debugging. | VARCHAR(255) |  |
| model_params | 97 | Holds the `agent_params` field value of the BidAgentResponse return by   the customer's bidding agent. If the line item uses Bid Models, this will   contain the cache results for the Bid Model lookup. This can be used for   debugging. Format => {key}={value},{key}={value}.. | VARCHAR(600) |  |
| data_center | 98 | Beeswax's data center responsible for processing the bid request/response   in question | VARCHAR(50) |  |
| billing_version | 99 | Internal | VARCHAR(50) |  |
| in_view | 100 | Determines if the impression is viewable or not | INT2 |  |
| is_measurable | 101 | Determines if the impression is measurable for viewability or not | INT2 |  |
| in_view_time_millis | 102 | States how much time the impression was in view, measured in miliseconds | INT8 |  |
| bidding_strategy_id | 103 | ID of the custom bidding strategy in Beeswax | VARCHAR(255) |  |
| bidding_strategy_params | 104 | Parameters passed along by the client for the custom bidding strategy in   Beeswax | VARCHAR(255) |  |
| exchange_predicted_view_rate | 105 | Estimated viewability rate, provided by the auction host | NUMERIC(18,6) |  |
| rx_timestamp | 106 | Impression Event received time in ET timezone | TIMESTAMP |  |
| battrs | 107 | Creative attributes that are blocked by the publisher, as declared by the   publisher | VARCHAR(255) |  |
| exchange_auction_id | 108 | Auction ID generated by the auction host ; different to that of Beeswax | VARCHAR(255) |  |
| rewarded | 109 | States whether the placement tag behind the impression is meant for   rewarded ads | INT2 |  |
| currency_rate | 110 | Currency exchange rate (in decimal) at the auction time | NUMERIC(18,10) |  |
| currency_code | 111 | Three letter currency codes setup in buzz | VARCHAR(10) |  |
| clearing_price_micros | 112 | Auction Clearing price(in micros) returned by exchange. This is the raw   media cost 1 Unit of Line Item's set Currency = 1,000,000 micros | INT8 |  |
| win_cost_micros | 113 | 1 Unit of Line Item's set Currency =   1,000,000 micros. Media Spend + Vendor Fees in USD$ (when 'Spend with Vendor Fees' is selected as the 'Budget Type' on the Line Item. If 'Spend' is selected, this will equal 'Media Spend')| INT8 |  |
| bid_price_micros | 114 | Bid price sent to the exchange (in micros, post-reduction). 1   Unit of Line Item's set Currency = 1,000,000 micros | INT8 |  |
| vendor_fee_micros | 115 | Vendor fee in micros. 1 Unit of Vendor Fee's set Currency = 1,000,000   micros | INT8 |  |
| viewability_vendor_name | 116 | Vendor used for providing viewability metrics | VARCHAR(10) |  |
| conversion_update_time | 117 | Formerly used internally | TIMESTAMP |  |
| companion_clicks | 118 | Set to 1 if the video's companion banner received a click | INT2 |  |
| companion_views | 119 | Set to 1 if the video's companion banner served an impression | INT2 |  |
| banner_width | 120 | Width of the impression in pixels | INT4 |  |
| banner_height | 121 | Height of the impression in pixels | INT4 |  |
| bid_floor_micros | 122 | The floor or lowest allowable clearing price of the auction. 1 USD =   1,000,000 micros | INT8 |  |
| bid_floor_currency | 123 | If the bid floor is specified and multiple currencies are supported per   bid request, the currency of the bid floor using ISO-4217 codes | VARCHAR(10) |  |
| display_manager | 124 | Name of the ad mediation partner, SDK technology, or player responsible   for rendering ad (typically video or mobile). Used by some ad servers to   customize ad code by partner. | VARCHAR(255) |  |
| display_manager_ver | 125 | Version of display_manager | VARCHAR(255) |  |
| exchange_device_make | 126 | Device make provided by the exchange, e.g. "Apple" | VARCHAR(255) |  |
| exchange_device_model | 127 | Device model provided by the exchange, e.g. "iPhone" | VARCHAR(255) |  |
| line_item_alt_id | 128 | Alternative ID in Buzz of the Line Item | VARCHAR(255) |  |
| page_url | 129 | URL of the page responsible for the auction | VARCHAR(255) |  |
| auction_type | 130 | If 1, first price auction. If 2, second price auction. Additional auction   types can be defined as per the exchange's business rules | INT4 |  |
| publisher_id | 131 | Publisher ID on the exchange. Prefixed with the exchange handle for   uniqueness | VARCHAR(255) |  |
| ads_txt | 132 | Ads.txt status for the request. It is an enum field, and can be one of the following values: Unauthorized, Authorized - Direct, Authorized - Reseller, Unknown, Authorized. See here for more information https://hub.freewheel.tv/display/BW/Ads.txt+and+App-ads.txt+Targeting | VARCHAR(20) |  |
| bid_modifier_id | 133 | ID of the Bid Modifier in Buzz | INT8 |  |
| bid_modifier_multipliers_product | 134 | Combined bid modifier multiplier applied to the bid | NUMERIC(18.6) |  |
| matched_user_groups | 135 | Matched user IDs for match tables hosted by Beeswax | VARCHAR(255) |  |
| ipv6_address | 136 | IPv6 address provided by the exchange during the auction. When no IPv6   address is present, the value is set to '0:0:0:0:0:0:0:0' | VARCHAR(255) |  |
| flight_id | 137 | ID of the Line Item Flight in Buzz (if present) | INT4 |  |
| user_id_hashed | 138 | GDPR-compliant hashed user_id | VARCHAR(255) |  |
| ip_address_hashed | 139 | GDPR-compliant hashed ip | VARCHAR(255) |  |
| ipv6_address_hashed | 140 | GDPR-compliant hashed ipv6 | VARCHAR(255) |  |
| is_gdpr | 141 | When this field is set to true, Beeswax has determined that this request   needs to comply with GDPR | INT2 |  |
| gdpr_consent_string | 142 | The raw IAB GDPR consent string as provided in the bid request | VARCHAR(255) |  |
| targeted_segments | 143 | Beeswax segment ID; contains all segments the user qualifies for that   were also targeted on the line item that won | VARCHAR(600) |  |
| clicks_ip_address | 144 | Comma delimited list of all unique IP adresses of all clicks (regular and   companion) associated with this impression | VARCHAR(255) |  |
| request_id | 145 | Unique ID for every bid request in the system. A joining key for all the   events associated with the bid request, like impression, clicks, and   activities. Note that it is possible to have multiple auction_ids for a   single request_id | VARCHAR(255) |  |
| person_linked_ids | 146 | Deprecated; will not be populated. | VARCHAR(600) |  |
| household_linked_ids | 147 | Deprecated; will not be populated. | VARCHAR(600) |  |
| video_protocols | 148 | Comma-separated list of video protocols that are accepted by the   publisher | VARCHAR(255) |  |
| clicks_user_id | 149 | The user ID captured on the click event | VARCHAR(255) |  |
| clicks_user_id_hashed | 150 | The user ID (hashed) captured on the click event | VARCHAR(255) |  |
| user_time_of_week | 151 | Time of week in GPS weekly time (minutes since Sunday midnight) of the   corresponding Bid Request in the user's local timezone. | INT4 |  |
| bot_clicks | 152 | Set to 1 if a click is suspected to originate from bot traffic | INT2 |  |
| bid_time_utc | 153 | Time of bid request sent, in UTC timezone | TIMESTAMP |  |
| rx_timestamp_utc | 154 | Time of receipt of the Impression Event, in UTC timezone | TIMESTAMP |  |
| test_group_id | 155 | ID of the Test Group the user fell into within the test plan. Should   match the Test Group assigned to the line item | INT4 |  |
| experiment_user_index | 156 | Random number between 1-1000 assigned to a user. Used for test group   assignment | INT4 |  |
| test_plan_id | 157 | ID of the Test Plan associated with the campaign | INT4 |  |
| inventory_source_user_id | 158 | Unique consumer ID of the user, as defined by the exchange. | VARCHAR(255) |  |
| mccmnc | 159 | Mobile carrier as defined by the concatenated MCC-MNC code. | VARCHAR(255) |  |
| us_privacy | 160 | US Privacy String as defined by the IAB CCPA Compliance Framework, and   used to define the regulatory context governing the personal data contained   within the associated bid request. | VARCHAR(255) |  |
| geo_type | 161 | LocationType, how the geographic information was determined | VARCHAR(20) |  |
| video_placement | 162 | The placement of the video impression (e.g., In-Stream) | VARCHAR(255) |  |
| publisher_name | 163 | Publisher Name as specified on the OpenRTB request. | VARCHAR(255) |  |
| freq_cap_id_type | 164 | Comma-separated list of the ID types that were used to perform frequency   capping for the impression | VARCHAR(255) |  |
| campaign_alt_id | 165 | Alternative ID in Buzz of the Campaign | VARCHAR(255) |  |
| exchange_imp_id | 166 | The ID of the Impression that was won. Relevant for multi-impression   auctions. Derived from OpenRTB's Impression ID object. | VARCHAR(255) |  |
| ua | 167 | The Useragent of the impression | VARCHAR(255) |  |
| seller_id | 168 | The value of the corresponding seller in sellers.json files. Only   populated when the exchange uses a different value for this than in Publisher   ID. | VARCHAR(255) |  |
| deal_bid_floors | 169 | Bid floor of the winning deal ID | VARCHAR(255) |  |
| site_referrer | 170 | The referrer to the site the auction occurred on. | VARCHAR(255) |  |
| bid_shade | 171 | The Bid Shade Status of the won impression. Will be one of: NOT_ELIGIBLE   - Line Item was ineligible for bid shading BID_SHADED - Line Item had its bid   shaded. CONTROL_GROUP - Line Item was eligible for bid shading but was   selected for the control group of the algorithm. | VARCHAR(255) |  |
| bid_shade_reduction_micros | 172 | Value the bid was shaded by in micros. | INT8 |  |
| video_mutes | 173 | Count of Video muted events. | INT8 |  |
| video_unmutes | 174 | Count of Video unmuted events. | INT8 |  |
| video_pauses | 175 | Count of Video pause events. | INT8 |  |
| video_resumes | 176 | Count of Video resume events. | INT8 |  |
| video_fullscreens | 177 | Count of Video fullscreen events. | INT8 |  |
| video_closes | 178 | Count of Video close events. | INT8 |  |
| impression_ip_address | 179 | The IP address of the impression; contrasted to ip_address, which derives   its IP from the bid request. | VARCHAR(255) |  |
| video_api | 180 | List of supported API frameworks for this impression. | VARCHAR(255) |  |
| bid_shading_fee_type | 181 | The Bid Shading Fee Type for the Impression. Will be one of: N/A: No bid   shading was used on the impression. VENDOR_FEE: The impression was using a   CUSTOMER_BILLABLE seat and the bid shading fee will be charged as a vendor   fee. INCLUDED_IN_WIN_PRICE: The impression was using a BEESWAX_BILLABLE seat   and the bid shading fee will be added to the media spend. | VARCHAR(255) |  |
| bid_shading_fee_micros_usd | 182 | The bid shading fee charged for the impression expressed in micros, in   USD. 1 USD = 1,000,000 micros | INT8 |  |
| bid_shading_fee_micros | 183 | The bid shading fee charged for the impression expressed in micros, in   local currency of the line item. 1 Unit of Currency = 1,000,000 micros | INT8 |  |
| require_native_video | 184 | If the creative for the impression is of type Native, this field will be   set to 1 when a video asset is required. The field will be 0 in all other   cases. | INT2 |  |
| is_gdpr_consented | 185 | Whether the auction is regulated by GDPR AND the customer has been   granted consent by the end user. | INT2 |  |
| targeted_lat_long_lists | 186 | The names of the lat/long lists specified that were targeted and matched   on the given request. | VARCHAR(255) |  |
| qag_media_rating | 187 | If defined, contains the QAG Media Rating of the content as defined by   OpenRTB spec. | VARCHAR(255) |  |
| media_spend_micros | 188 | The total cost of media for the impression expressed in micros in the the   local currency of the line item. 1 Unit of Currency = 1,000,000 micros | INT8 |  |
| media_spend_micros_usd | 189 | The total cost of media for the impression expressed in micros in US   dollars. 1 Unit of Currency = 1,000,000 micros | INT8 |  |
| guaranteed | 190 | Indicates whether a bid request is guaranteed or not. | INT2 |  |
| creative_alt_id | 191 | If set, the alternative ID of the creative that won the auction will   populate in this column. | VARCHAR(255) |  |
| creative_name | 192 | The name of the creative as specified in Buzz. | VARCHAR(255) |  |
| lat_long_list_item_ids | 193 | Comma-separated list of unique keys describing the matching lat/long list   item IDs for this event. Formed as the cocatenation of the List ID and List   Item ID separated by a colon (:). e.g. buzz_key-10:9292 | VARCHAR(255) |  |
| lat_long_list_item_names | 194 | Comma-separated list of names (if set) for the the matching lat/long list   item IDs for this event. Displayed in the same order as the IDs in the   previous column. If no name is set for the matched list item then the field   will be set to an empty string for each given list item id. If multiple list   items match this field may have multiple commas with no values in it. | VARCHAR(255) |  |
| click_rx_timestamp_utc | 195 | If a click was joinable to this impression, this column contains the   timestamp of receipt of the event. | TIMESTAMP |  |
| bcat | 196 | Blocked advertiser categories using the IAB content categories. | VARCHAR(255) |  |
| platform_device_hwv | 197 | The hardware version as specified in the OpenRTB specification | VARCHAR(255) |  |
| platform_device_language | 198 | Browser language using ISO-639-1-alpha-2 as specified in the OpenRTB   specification | VARCHAR(255) |  |
| platform_device_w | 199 | The physical device's width in pixels as specified in the OpenRTB   specification | INT4 |  |
| platform_device_h | 200 | The physical device's height in pixels as specified in the OpenRTB   specification | INT4 |  |
| platform_device_ppi | 201 | The device's screen size as express in pixels per inch, as specified in   OpenRTB specification | INT4 |  |
| platform_device_pxratio | 202 | The ratio of physical pixels to device independent pixels, as specified   in OpenRTB specification | NUMERIC(18,6) |  |
| invalid_impression | 203 | Specifies whether an impression may be viewed as IVT contingent on vendor   rules. | INT2 |  |
| is_invalid_measurable | 204 | Specifies whether an impression was measurable for IVT tracking purposes. | INT2 |  |
| invalid_automated_browser | 205 | Flags whether an IVT impression was viewed as originating from an   automated browser. | INT2 |  |
| invalid_incongruous_browser | 206 | Flags whether an IVT impression was viewed as originating from an   incongruous browser. | INT2 |  |
| invalid_data_center_traffic | 207 | Flags whether an IVT impression was viewed as originating from a data   center. | INT2 |  |
| invalid_impression_vendor_name | 208 | The name of the vendor from which IVT fields were populated. | VARCHAR(10) |  |
| experiment_id_type | 209 | The ID type used for segregation of impressions for Beeswax's experiment   feature. | VARCHAR(255) |  |
| deal_auction_type | 210 | If the impression was purchased via a deal, this logs the auction type   for the deal. 1 = First Price, 2 = Second Price, 3 = Fixed Price. Overrides   "auction_type |  |  |
| account_level_revenue_share_fee_type | 211 | If using the account-level revenue share feature, this column populates   whether the fee is expressed as a reduction or fee. | VARCHAR(255) |  |
| account_level_revenue_share_percent_micros | 212 | If using the account-level revenue share feature, this column populates   the percentage of the rev share for the given impression in micros. | INT8 |  |
| account_level_revenue_share_micros_usd | 213 | As above, but populates the calcualted value of the rev share in USD as   expressed in micros. | INT8 |  |
| account_level_revenue_share_micros | 214 | As above, but populates the calcualted value of the rev share in the   local currency as expressed in micros. | INT8 |  |
| tmax | 215 | The required time in milliseconds for the bid to respond to the exchange   to be considered in the auction | INT4 |  |
| video_skippable | 216 | If the ad is a video ad, this field indicates whether the creative   trafficked could have been skippable. | INT2 |  |
| is_skadnetwork | 217 | Flags whether the inventory is SKAdNetwork enabled. | INT2 |  |
| dnt | 218 | Do Not Track | INT4 |  |
| lmt | 219 | Limit Ad Tracking (LMT) is a device-level opt-out setting, that allows   users to limit the amount of information sent from their device to ad   exchanges (including omitting their device ID) | INT2 |  |
| banner_format | 220 | Comma-separated list of banner formats (wxh) that are accepted by the publisher. If none are specified, use the banner_height and banner_width fields. If banner_width, banner_height and banner_format are provided, the banner_format array should take precedence. | VARCHAR(255) |  |
| content_id | 221 | ID uniquely identifying the content | VARCHAR(255) |  |
| content_episode | 222 | Episode number | VARCHAR(255) |  |
| content_title | 223 | Content title | VARCHAR(255) |  |
| content_series | 224 | Content series | VARCHAR(255) |  |
| content_season | 225 | Content season | VARCHAR(255) |  |
| content_genre | 226 | Genre that best describes the content | VARCHAR(255) |  |
| content_contentrating | 227 | Content rating (e.g., MPAA) | VARCHAR(255) |  |
| content_keywords | 228 | Comma separated list of keywords describing the content | VARCHAR(255) |  |
| content_livestream | 229 | 0 = not live, 1 = content is live (e.g., stream, live blog) | INT4 |  |
| content_len | 230 | Length of content in seconds; appropriate for video or audio | VARCHAR(255) |  |
| content_network_id | 231 | ID of the network the content is on. This may not be a unique identifier   across all supply sources | VARCHAR(255) |  |
| content_network_name | 232 | Network the content is on (e.g., a TV network like “ABC") | VARCHAR(255) |  |
| content_network_domain | 233 | The primary domain of the network (e.g. “abc.com” in the case of the   network ABC). | VARCHAR(255) |  |
| content_channel_id | 234 | ID of the channel the content is on. This may not be a unique identifier   across all supply sources | VARCHAR(255) |  |
| content_channel_name | 235 | Channel the content is on (e.g., a local channel like “WABC-TV") | VARCHAR(255) |  |
| content_channel_domain | 236 | The primary domain of the channel (e.g. “abc7ny.com” in the case of the   local channel WABC-TV) | VARCHAR(255) |  |
| content_cat | 237 | Array of IAB content categories that describe the content | VARCHAR(255) |  |
| ip_conversions | 238 | Number of IP conversions associated to a particular impression | INT4 |  |
| ip_conversion_order | 239 | IP conversion order, constitutes how many orders a particular IP   conversion represents; info provided by the advertiser in Beeswax UI/API | NUMERIC(18,6) |  |
| ip_conversion_value | 240 | Value of a given IP conversion as ispecified by the advertiser in Beeswax   UI/API | NUMERIC(18,6) |  |
| master_revenue_share_percent_micros | 241 | If using a master revenue share, a micro value percentage represent the   revenue share being taken. | INT8 |  |
| master_revenue_share_micros_usd | 242 | Master revenue share amount in USD. | INT8 |  |
| master_revenue_share_micros | 243 | Master revenue share amount in bid currency. | INT8 |  |
| total_vendor_fees_micros_usd | 244 | Total fee amount withheld in USD, inclusive of master revenue share. | INT8 |  |
| total_vendor_fees_micros | 245 | Total fee amount withheld in bid currency, inclusive of master revenue   share. | INT8 |  |
| delivery_modifier_id | 246 | The ID of the Delivery Modifier. | INT4 |  |
| delivery_model_id | 247 | The ID of the Delivery Model. | VARCHAR(255) |  |
| bid_model_id | 248 | The ID of the Bid Model, formatted like   {buzz_key}-{bid_model_id}-(bid_model_version}. | VARCHAR(255) |  |
| bid_model_params | 249 | The cache results for the Bid Model lookup, formatted like   {key}={value},{key}={value} | VARCHAR(600) |  |
| bid_agent_id | 250 | Holds the agent_id field value of the BidAgentResponse returned by the   customer's bidding agent. | VARCHAR(255) |  |
| bid_agent_params | 251 | Holds the agent_params field value of the BidAgentResponse return by the   customer's bidding agent. | VARCHAR(600) |  |
| topics_id | 252 | Represents the Topics ID from the taxonomy identified by the Taxonomy   Version. | VARCHAR(255) |  |
| topics_taxonomy_version | 253 | The ID associated with a taxonomy that is registered centrally with the   IAB Tech Lab in Enumeration of Taxonomies. | VARCHAR(255) |  |
| audio_plays | 254 | Set to 1 if audio ad is played. | INT4 |  |
| audio_q1s | 255 | Set to 1 if audio ad is watched through the first quartile. | INT4 |  |
| audio_midpoints | 256 | Set to 1 if audio ad is watched through the second quartile. | INT4 |  |
| audio_q3s | 257 | Set to 1 if audio ad is watched through the third quartile. | INT4 |  |
| audio_completes | 258 | Set to 1 if audio ad is watched through the fourth quartile. | INT4 |  |
| audio_skips | 259 | Set to 1 if audio ad is skipped. | INT4 |  |
| bw_content_genre | 260 | The mapped Beeswax Content Genre from the taxonomy. This field will only   be populated for video bid requests. | VARCHAR(255) |  |
| audio_startdelay | 261 | Indicates the start delay in seconds for pre-roll, mid-roll, or post-roll   audio ad placements. | INT4 |  |
| audio_minbitrate | 262 | The minimum allowed bitrate, in Kbps. | INT4 |  |
| audio_maxbitrate | 263 | The maximum allowed bitrate, in Kbps. | INT4 |  |
| audio_feed | 264 | The type of feed for audio requests. | VARCHAR(50) |  |
| audio_companion_required | 265 | A banner companion ad is required to accompany the audio ad: 0=false, 1=true, -1=unknown, not provided, null, etc. | INT4 |  |
| bidreq_universal_ids | 266 | Comma-separated list of encrypted ID5 universal ID values | VARCHAR(255) |  |
| video_plcmt | 267 | The placement of the video impression. 1=INSTREAM, 2=ACCOMPANYING CONTENT, 3=INTERSTITIAL, 4=NO CONTENT/STANDALONE | VARCHAR(255) |  |
| app_ads_txt | 268 | App Ads.txt status for the request. It is an enum field, and can be one of the following values: Unauthorized, Authorized - Direct, Authorized - Reseller, Unknown, Authorized  | VARCHAR(50) |  |
| schain_complete | 269 | Flag indicating whether the chain contains all nodes involved in the transaction leading back to the owner of the site, app or other medium of the inventory.  | INT8 |  |
| schain_version | 270 | Version of the supply chain specification in use. Applies to the entire schain object.  | VARCHAR(50) |  |
| schain_node_asi | 271 | The canonical domain name of the SSP, Exchange, Header Wrapper, etc. system that bidders connect to. This should be the same value as used to identify sellers in an ads.txt file if one exists. This field represents values across all nodes in the object in the form of a comma separated varchar array. The index of each value corresponds to the index of each node on the schain object. For example, if this field is reprsented as '1.com', '2.com' then domain 1.com corresponds with the 1st node in the schain, while 2.com represents the 2nd.  | VARCHAR(1024) |  |
| schain_node_sid | 272 | Identifier associated with the seller or reseller account within the advertising system. This field represents values across all nodes in the object in the form of a comma separated varchar array. The index of each value corresponds to the index of each node on the schain object. | VARCHAR(1024) |  |
| schain_node_rid | 273 | OpenRTB RequestId of the request as issued by this seller. This field represents values across all nodes in the object in the form of a comma separated varchar array. The index of each value corresponds to the index of each node on the schain object. | VARCHAR(1024) |  |
| schain_node_name | 274 | Name of the company (the legal entity) that is paid for inventory transacted under the given seller_id. This field represents values across all nodes in the object in the form of a comma separated varchar array. The index of each value corresponds to the index of each node on the schain object. | VARCHAR(1024) |  |
| schain_node_domain | 275 | Business domain name of the entity represented by this node. This value is optional and is not included if it exists in the advertising system’s sellers.json file. This field represents values across all nodes in the object in the form of a comma separated varchar array. The index of each value corresponds to the index of each node on the schain object. | VARCHAR(1024) |  |
| schain_node_hp | 276 | Indicates whether this node will be involved in the flow of payment for the inventory. This field represents values across all nodes in the object in the form of a comma separated varchar array. The index of each value corresponds to the index of each node on the schain object. | VARCHAR(1024) |  |
| schain_node_internal_sid | 277 | Identifier associated with the seller or reseller account within the advertising system. The SID is augmented to include the exchange handle to match the seller_id field in logs. This field represents values across all nodes in the object in the form of a comma separated varchar array. The index of each value corresponds to the index of each node on the schain object.​ | VARCHAR(1024) |  |
| sellers_json_seller_name | 278 | Seller Name listed on the sellers.json file. ​ | VARCHAR(1024) |  |
| sellers_json_status | 279 | Whether a match was found when looking up the Publisher ID in sellers.json files. Values include: Unknown: No Publisher ID was passed in the bid request to lookup against sellers. Seller Not Found: No match was found to the Publisher ID passed in the bid request. Authorized: This seller is authorized based on the sellers.json table, but the seller type cannot be identified for various reasons. Authorized - Publisher: A match was found to the Publisher ID and the Seller Type is "Publisher". Authorized - Intermediary: A match was found to the Publisher ID and the Seller Type is "Intermediary". Authorized - Both: A match was found to the Publisher ID and the Seller Type is "Both"​ | VARCHAR(50) |  |
| sellers_json_seller_type | 280 | The value pulled from the sellers.json file. Options include: Publisher: The inventory sold through this account is owned by the named entity and the advertising system pays them directly. Intermediary: The inventory sold through this account is not owned by the named entity, or the advertising systems does not pay them directly. Both: Both publisher and intermediary inventory are transacted by this account.​ | VARCHAR(50) |  |
| sellers_json_mapped_name | 281 | The Seller Name listed in the in the sellers.json file mapped to a taxonomy to consolidate into a single standardized name. The taxonomy does not account for all sellers names. The most commonly passed seller names have been prioritized. It's recommended to use both the Seller Name and Mapped Seller Name dimensions. | VARCHAR(1024) |  |
| audio_delivery | 282 | Supported delivery methods (STREAMING, PROGRESSIVE, DOWNLOAD, ALL).| VARCHAR(255) |  |
| bw_audio_content_genre | 283 | The mapped Beeswax Audio Content Genre from the taxonomy. This field will only be populated for audio bid requests | VARCHAR(255) |  |
