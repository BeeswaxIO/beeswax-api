| Header | Position | Definition | SQL Datatype | DDL Desc |
|---|---|---|---|---|
| ad_position | 1 | If applicable, ad position on page | VARCHAR(255) |  |
| app_bundle | 2 | Application bundle or package name (e.g., com.foo.mygame). This is intended to be a unique ID across multiple exchanges. | VARCHAR(255) |  |
| app_id | 3 | Application ID on the exchange. For uniqueness, Uses ad exchange/SSP identifier as prefix e.g. pm/ representing pubmatic | VARCHAR(255) |  |
| app_name | 4 | Mobile app name | VARCHAR(255) |  |
| auction_id | 5 | Unique ID for every auction in the system. A joining key for all the events associated with the auction, like impression, clicks, and activities. | VARCHAR(255) |  |
| bid_time | 6 | Time of bid request sent, YYYY-MM-DD HH:MM:SS in ET timezone | TIMESTAMP | YYYY-MM-DD HH24:MI:SS.MS in ET |
| category | 7 | CSV of IAB-defined content categories: http://www.iab.com/guidelines/iab-quality-assurance-guidelines-qag-taxonomy/; determine type of content associated with a particular slice of inventory | VARCHAR(255) |  |
| content_coppa_flag | 8 | Children’s Online Privacy Protection Act (COPPA) Flag; inventory with this flag carries several ad quality limitations | BOOLEAN |  |
| content_language | 9 | Language in which content associated to the impression is written (as declared by the publisher) | VARCHAR(255) |  |
| content_rating | 10 | Content parental rating (as declared by the publisher) | VARCHAR(255) |  |
| domain | 11 | Domain name from which a given impression originated | VARCHAR(255) |  |
| environment_type | 12 | Environment type (APP or WEB) | VARCHAR(255) |  |
| geo_city | 13 | City geo code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_country | 14 | Country geo name IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_metro | 15 | Metro geo code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_region | 16 | Geo region name IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| geo_zip | 17 | Zip code IP address. MaxMindDB Lookup data | VARCHAR(255) |  |
| inventory_interstitial | 18 | determines if ad tag responsible for the impression accepts interstitial creatives or not; 1 for yes, 0 for no | BOOLEAN |  |
| inventory_source | 19 | Inventory source - exchange name | VARCHAR(255) |  |
| inventory_source_relationship | 20 | Inventory source relationship | VARCHAR(255) |  |
| ip_address | 21 | IP address provided by the exchange during the auction. When no IPv4 address is present, the value is set to '0.0.0.0' | VARCHAR(255) |  |
| ip_range | 22 | IP address provided by the exchange during the auction (same as ip_address) | VARCHAR(255) |  |
| placement | 23 | Placement ID/name, as provided by the publisher. Prefixed with exchange handle. | VARCHAR(255) |  |
| platform_bandwidth | 24 | Shows whether the browser is using wifi or carrier to establish connection with internet to generate the impression | VARCHAR(255) |  |
| platform_browser | 25 | Name of browser used during the auction for the impression at hand | VARCHAR(255) |  |
| platform_browser_version | 26 | Version of browser used to during the auction for the impression at hand | VARCHAR(255) |  |
| platform_carrier | 27 | If the device is using a mobile carrier to establish internet connection, this field will identify which carrier is used | VARCHAR(255) |  |
| platform_device_didmd5 | 28 | Hardware device ID (e.g., IMEI); hashed via MD5 | VARCHAR(255) |  |
| platform_device_didsha1 | 29 | Hardware device ID (e.g., IMEI); hashed via SHA1 | VARCHAR(255) |  |
| platform_device_dpidmd5 | 30 | Platform device ID (e.g., Android ID); hashed via MD5 | VARCHAR(255) |  |
| platform_device_dpidsha1 | 31 | Platform device ID (e.g., Android ID); hashed via SHA1 | VARCHAR(255) |  |
| platform_device_idfa | 32 | iOS app ID; "Identifier for Advertisers"; deprecated | VARCHAR(255) |  |
| platform_device_ifa | 33 | ID sanctioned for advertiser use in the clear (i.e., not hashed) | VARCHAR(255) |  |
| platform_device_make | 34 | Make of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_model | 35 | Model of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_screen_size | 36 | Screensize of the device used to generate the impression | VARCHAR(255) |  |
| platform_device_type | 37 | Type of the device used to generate the impression | VARCHAR(255) |  |
| platform_js | 38 | Indicates whether the browser supports JavaScript or not | BOOLEAN |  |
| platform_os | 39 | Operating system of the device used to generate the impression | VARCHAR(255) |  |
| platform_os_version | 40 | Operating system version of the device used to generate the impression | VARCHAR(255) |  |
| segment_id | 41 | Beeswax segment ID | VARCHAR(600) |  |
| segment_user_id | 42 | Beeswax segment user ID | INT2 |  |
| site_id | 43 | ID of the site that generated the impression, as provided by the publisher. Prefixed with exchange handle for uniqueness. | VARCHAR(255) |  |
| site_name | 44 | Name of the site that generated the impression, as provided by the publisher | VARCHAR(255) |  |
| time_of_week | 45 | Time of week in GPS weekly time during which the impression occurred; internal | INT2 |  |
| user_id | 46 | Primary user ID on the request. For web inventory: will populate with a beeswax cookie ID if one is found, and fall back to device ID if not. For app inventory: will populate with a device ID. | VARCHAR(255) |  |
| video_boxing_allowed | 47 | Indicates if letter-boxing of 4:3 content into a 16:9 window is  allowed, where 0 = no, 1 = yes | BOOLEAN |  |
| video_companion_required | 48 | A banner companion ad is required to accompany the video ad: 0=false, 1=true | BOOLEAN |  |
| video_playback_method | 49 | Video playback method, as determined by the publisher. | VARCHAR(255) |  |
| video_player_size | 50 | Video player size | VARCHAR(255) |  |
| video_start_delay | 51 | Indicates the start delay in seconds for pre-roll, mid-roll, or  post-roll video ad placements | INT2 |  |
| test | 52 | Indicator of test mode in which auctions are not billable, where 0 = live mode, 1 = test mode | BOOLEAN |  |
| placement_type | 53 | Placement type, indicates whether the placement is meant for banner, video ads, or both | VARCHAR(255) |  |
| geo_lat | 54 | Latitude associated with the impression | VARCHAR(50) |  |
| geo_long | 55 | Longitude associated with the impression | VARCHAR(50) |  |
| video_min_duration | 56 | Minimum duration of the video creative, as allowed by the publisher | INT4 |  |
| video_max_duration | 57 | Maximum duration of the video creative, as allowed by the publisher | INT4 |  |
| video_player_width | 58 | Width of the video player that is responsible for generating the impression | INT4 |  |
| video_player_height | 59 | Height of the video player that is responsible for generating the impression | INT4 |  |
| banner_width | 60 | Width of the banner placement tag | INT4 |  |
| banner_height | 61 | Height of the banner placement tag | INT4 |  |
| banner_width_max | 62 | Maximum width of the banner placement, as allowed by the publisher | INT4 |  |
| banner_height_max | 63 | Maximum height of the banner placement, as allowed by the publisher | INT4 |  |
| banner_width_min | 64 | Minimum width of the banner placement, as allowed by the publisher | INT4 |  |
| banner_height_min | 65 | Minimum height of the banner placement, as allowed by the publisher | INT4 |  |
| dnt | 66 | Do Not Track | INT4 |  |
| geo_type | 67 | LocationType, how the geographic information was determined | VARCHAR(20) |  |
| bid_time_epoch_in_usecs | 68 | bid timestamp(epoch) with microsecond precision. Allows the customer to calculate the bid_time in any timezone instead of relying on `bid_time` field which is ET timezone | INT8 |  |
| page_url | 69 | URL of the page responsible for the auction | VARCHAR(255) |  |
| exchange_predicted_view_rate | 70 | Predicted Viewability Rate of the impression within the auction, as determined by the exchange-auctioner | NUMERIC(18,6) |  |
| available_deal_ids | 71 | Comma-separated list of all the available deal IDs on the associated Bid Request | VARCHAR(1048576) |  |
| battrs | 72 | Creative attributes that are blocked by the publisher, as declared by the publisher | VARCHAR(255) |  |
| exchange_auction_id | 73 | Auction ID generated by the auction host ; different to that of Beeswax | VARCHAR(255) |  |
| rewarded | 74 | States whether the placement tag behind the impression is meant for rewarded ads | INT2 |  |
| ua | 75 | User agent header that is passed along by the browser to the auction host when an impression is generated | VARCHAR(255) |  |
| bid_floor_micros | 76 | The floor or lowest allowable clearing price of the auction. 1 USD = 1,000,000 micros | INT8 |  |
| bid_floor_currency | 77 | If the bid floor is specified and multiple currencies are supported per bid request, the currency of the bid floor using ISO-4217 codes | VARCHAR(10) |  |
| display_manager | 78 | Name of the ad mediation partner, SDK technology, or player responsible for rendering ad (typically video or mobile). Used by some ad servers to customize ad code by partner. | VARCHAR(255) |  |
| display_manager_ver | 79 | Version of display_manager | VARCHAR(255) |  |
| exchange_device_make | 80 | Device make provided by the exchange, e.g. "Apple" | VARCHAR(255) |  |
| exchange_device_model | 81 | Device model provided by the exchange, e.g. "iPhone" | VARCHAR(255) |  |
| user_id_type | 82 | A string representation (enum) of the type of user ID. "BEESWAX" for cookie ID. e.g. AD_ID, IDFA, IDFA_SHA1, BEESWAX | VARCHAR(20) |  |
| auction_type | 83 | If 1, first price auction. If 2, second price auction. Additional auction types cna be defined as per the exchange's business rules | INT4 |  |
| publisher_id | 84 | Publisher ID on the exchange. Prefixed with the exchange handle for uniqueness | VARCHAR(255) |  |
| ads_txt | 85 | Ads.txt status for the request. It is an enum field, and can be one of the following values: UNKNOWN - The request was not augmented by the ads.txt augmentor (should never happen) NO_DOMAIN - The request does not contain a domain, either because it is not a web request (ie it is an app or native request) or it is a web request but does not contain a domain NO_ADS_TXT_FILE - The request's domain does not have an Ads.txt file ADS_TXT_NOT_SCANNED - We have not looked up the Ads.txt file for the request's domain NO_ADVERTISING_ALLOWED - The request's domain does not allow any advertising MISSING_PUB_ID - The request is missing a publisher id so we cannot check its Ads.txt status NOT_AUTH - The request's domain does have an Ads.txt file, but it does not allow advertising from this exchange / publisher ID combination AUTH_RESELLER - The domain's Ads.txt file allows this exchange / publisher ID to resell advertising AUTH_DIRECT - The domain's Ads.txt file allows this exchange / publisher ID to advertise directly | VARCHAR(20) |  |
| matched_user_groups | 86 | Matched user IDs for match tables hosted by Beeswax | VARCHAR(255) |  |
| ipv6_address | 87 | IPv6 address provided by the exchange during the auction. When no IPv6 address is present, the value is set to '0:0:0:0:0:0:0:0' | VARCHAR(255) |  |
| user_id_hashed | 88 | GDPR-compliant hashed user_id | VARCHAR(255) |  |
| ip_address_hashed | 89 | GDPR-compliant hashed ip | VARCHAR(255) |  |
| ipv6_address_hashed | 90 | GDPR-compliant hashed ipv6 | VARCHAR(255) |  |
| is_gdpr | 91 | When this field is set to true, Beeswax has determined that this request needs to comply with GDPR | INT2 |  |
| gdpr_consent_string | 92 | The raw IAB GDPR consent string as provided in the bid request | VARCHAR(255) |  |
| request_id | 93 | Unique ID for every bid request in the system. A joining key for all the events associated with the bid request, like impression, clicks, and activities. Note that it is possible to have multiple auction_ids for a single request_id | VARCHAR(255) |  |
| person_linked_ids | 94 | Deprecated; will not be populated. | VARCHAR(600) |  |
| household_linked_ids | 95 | Deprecated; will not be populated. | VARCHAR(600) |  |
| video_protocols | 96 | Comma-separated list of video protocols that are accepted by the publisher | VARCHAR(255) |  |
| banner_top_frame | 97 | Indicates if the banner is in the top frame as opposed to an iframe | INT2 |  |
| user_time_of_week | 98 | Time of week in GPS weekly time during which the impression occurred using the user's timezone; internal | INT4 |  |
| bid_time_utc | 99 | Time of bid request sent, in UTC timezone | TIMESTAMP | YYYY-MM-DD HH24:MI:SS.MS in UTC |
| inventory_source_user_id | 100 | Unique consumer ID of the user, as defined by the exchange. | VARCHAR(255) |  |
| mccmnc | 101 | Mobile carrier as defined by the concatenated MCC-MNC code. | VARCHAR(255) |  |
| us_privacy | 102 | US Privacy String as defined by the IAB CCPA Compliance Framework, and used to define the regulatory context governing the personal data contained within the associated bid request. | VARCHAR(255) |  |
| video_placement | 103 | The placement of the video impression (e.g., In-Stream) | VARCHAR(255) |  |
| experiment_user_index | 104 | Random number between 1-1000 assigned to a user. Used for test group assignment | INT4 |  |
| publisher_name | 105 | Publisher Name as specified on the OpenRTB request. | VARCHAR(255) |  |
| carrier | 106 | The device's carrier as specified via the OpenRTB protocol | VARCHAR(255) |  |
| platform_device_ifa_type | 107 | The type of IFA in platform_device_ifa, per the IAB's IFA Guidelines. | VARCHAR(255) |  |
| deal_bid_floors | 108 | Comma-separated list of the bid floors for the available deal IDs | VARCHAR(255) |  |
| seller_id | 109 | The value of the corresponding seller in sellers.json files. Only populated when the exchange uses a different value for this than in Publisher ID. | VARCHAR(255) |  |
| data_center | 110 | The data center the auction was received by. | VARCHAR(255) |  |
| site_referrer | 111 | The referrer to the site the auction occurred on. | VARCHAR(255) |  |
| video_api | 112 | List of supported API frameworks for this impression. | VARCHAR(255) |  |
| require_native_video | 113 | Indicates whether the creative is native and requires a video creative | INT2 |  |
| is_gdpr_consented | 114 | Whether the auction is regulated by GDPR AND the customer has been granted consent by the end user. | INT2 |  |
| qag_media_rating | 115 | If defined, contains the QAG Media Rating of the content as defined by OpenRTB spec. | VARCHAR(255) |  |
| bcat | 116 | Blocked advertiser categories using the IAB content categories. | VARCHAR(255) |  |
| platform_device_hwv | 117 | Hardware Version of the Device sent via OpenRTB | VARCHAR(255) |  |
| platform_device_language | 118 | Browser language using ISO-639-1-alpha-2. Sent via OpenRTB | VARCHAR(255) |  |
| platform_device_w | 119 | Physical width of the screen in pixels | INT4 |  |
| platform_device_h | 120 | Physical height of the screen in pixels | INT4 |  |
| platform_device_ppi | 121 | Screen size as pixels per linear inch. | INT4 |  |
| platform_device_pxratio | 122 | The ratio of physical pixels to device independent pixels. | NUMERIC(18,6) |  |
| deal_ats | 123 | If the impression was purchased via a deal, this logs the auction type for all deals on the auction in the same order as the deal_ids column. 1 = First Price, 2 = Second Price, 3 = Fixed Price. Overrides "auction_type" |  |  |
| tmax | 124 | The required time in milliseconds for the bid to respond to the exchange to be considered in the auction | INT4 |  |
| video_skippable | 125 | If the ad is a video ad, this field indicates whether the creative trafficked could have been skippable. | INT2 |  |
| is_skadnetwork | 126 | Flags whether the inventory is SKAdNetwork enabled. | INT2 |  |
| lmt | 127 | Limit Ad Tracking (LMT) is a device-level opt-out setting, that allows users to limit the amount of information sent from their device to ad exchanges (including omitting their device ID) | INT2 |  |
| banner_format | 128 | Comma-separated list of banner formats (wxh) that are accepted by the publisher | VARCHAR(255) |  |
| content_id | 129 | ID uniquely identifying the content | VARCHAR(255) |  |
| content_episode | 130 | Episode number | VARCHAR(255) |  |
| content_title | 131 | Content title | VARCHAR(255) |  |
| content_series | 132 | Content series | VARCHAR(255) |  |
| content_season | 133 | Content season | VARCHAR(255) |  |
| content_genre | 134 | Genre that best describes the content | VARCHAR(255) |  |
| content_contentrating | 135 | Content rating (e.g., MPAA) | VARCHAR(255) |  |
| content_keywords | 136 | Comma separated list of keywords describing the content | VARCHAR(255) |  |
| content_livestream | 137 | 0 = not live, 1 = content is live (e.g., stream, live blog) | INT4 |  |
| content_len | 138 | Length of content in seconds; appropriate for video or audio | VARCHAR(255) |  |
| content_network_id | 139 | ID of the network the content is on. This may not be a unique identifier across all supply sources | VARCHAR(255) |  |
| content_network_name | 140 | Network the content is on (e.g., a TV network like “ABC") | VARCHAR(255) |  |
| content_network_domain | 141 | The primary domain of the network (e.g. “abc.com” in the case of the network ABC). | VARCHAR(255) |  |
| content_channel_id | 142 | ID of the channel the content is on. This may not be a unique identifier across all supply sources | VARCHAR(255) |  |
| content_channel_name | 143 | Channel the content is on (e.g., a local channel like “WABC-TV") | VARCHAR(255) |  |
| content_channel_domain | 144 | The primary domain of the channel (e.g. “abc7ny.com” in the case of the local channel WABC-TV) | VARCHAR(255) |  |
| content_cat | 145 | Array of IAB content categories that describe the content | VARCHAR(255) |  |
| ssai | 146 |  Indicates if server-side ad insertion is in use.  | INT4 |  |
| topics_id | 147 | Represents the Topics ID from the taxonomy identified by the Taxonomy Version. | VARCHAR(255) |  |
| topics_taxonomy_version | 148 | The ID associated with a taxonomy that is registered centrally with the IAB Tech Lab in Enumeration of Taxonomies. | VARCHAR(255) |  |
| bw_content_genre | 149 | The mapped Beeswax Content Genre from the taxonomy. This field will only be populated for video bid requests. | VARCHAR(255) |  |
| audio_startdelay | 150 | Indicates the start delay in seconds for pre-roll, mid-roll, or post-roll audio requests. | INT4 |  |
| audio_minbitrate | 151 | Minimum bitrate for audio requests, in Kbps. | INT4 |  |
| audio_maxbitrate | 152 | Maximum bitrate for audio requests, in Kbps. | INT4 |  |
| audio_feed | 153 | Type of feed for audio requests. | VARCHAR(50) |  |
| audio_companion_required | 154 | A banner companion ad is required to accompany the audio ad: 0=false, 1=true, -1=unknown, not provided, null, etc. | INT4 |  |
| bidreq_universal_ids | 155 | Comma-separated list of encrypted ID5 universal ID values | VARCHAR(255) |  |
| video_plcmt | 156 | The placement of the video impression. 1=INSTREAM, 2=ACCOMPANYING CONTENT, 3=INTERSTITIAL, 4=NO CONTENT/STANDALONE | VARCHAR(255) |  |
| wseat | 157 | *Currently not availble, field will be blank* White list of buyer seats allowed to bid on this impression. | VARCHAR(255) |  |
| deals_wseat | 158 | *Currently not availble, field will be blank* Whitelist of buyer seats allowed to bid on this deal.  | VARCHAR(255) |  |
| freewheel_person_linked_ids | 159 | Deprecated; will not be populated. | INT4 |  |
| freewheel_household_linked_ids | 160 | Deprecated; will not be populated. | INT4 |  |
| freewheel_person_ids | 161 | Deprecated; will not be populated. | INT4 |  |
| freewheel_household_ids | 162 | Deprecated; will not be populated. | INT4 |  |
| app_ads_txt | 163 | App Ads.txt status for the request. It is an enum field, and can be one of the following values: Unauthorized, Authorized - Direct, Authorized - Reseller, Unknown, Authorized  | VARCHAR(50) |  |

