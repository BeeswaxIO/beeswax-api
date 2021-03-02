# Background

Bid models support several user based features: Targeted Segment, Segment Recency, and Frequency. These features and their use are outlined in this document.

* **Targeted Segment** allows users to adjust bid prices based on which targeted segment a user falls into. Only segments explicitly targeted by the line item are eligible features in the bid model. 

* **Segment Recency** allows customers to adjust bid prices based on how long ago a user was added to a particular segment. For example, if a user signs up for an automobile test drive they may be put into the “Auto Intender” segment. This person expressed interest and so the advertiser may want to bid much higher for them in the first few days, and less after that. This concept is the same as Segment Recency in targeting and is only available for 1st party segments

* **Frequency** allows customers to adjust bid prices based on how many times the user was exposed to a particular ad in the past. If a user has already seen the same ad three times, the customer may want to bid less on that user without setting a hard frequency cap.

# Applying User Based Features

## Targeted Segment
The Targeted Segment feature can be included in a prediction file like any other Bid Model feature. Unlike Bid Modifiers, Bid Models do not support the ‘dynamic’ segment option. This is because the Bid Model value is determined by a combination of features and Targeted Segment is only one of these. If a customer has a use case for dynamic Targeted Segments with Bid Models, a workaround is to remove Targeted Segment from the Bid Model and instead add a Bid Modifier targeting the segment dynamically.

**Log Header:** targeted_segment

The targeted_segment column takes segment IDs as values.

**Example:**

| targeted_segment | domain | value |
|------------|-----------------|------------------|
| canary-123 | espn.com | [expected bid ]|
| canary-456 | abc.com | [expected bid ]|
| ...        | ...             |...  |


## Segment Recency
Segment Recency introduces a new convention to Bid Models, as this feature requires two columns in order to be activated. One column specifies the segment and the other specifies the recency window.

* Note: Segment Recency cannot be used without also including the targeted_segment feature.

**Log Headers:** targeted_segment, segment_recency

The segment_recency value refers to a predefined recency window, as enumerated below. Since recency windows do not overlap, multiple Bid Model rows need to be created in order to define Segment Recency across a broader time horizon.

In the following example, the three canary-456 Segment Recency definitions functionally mean, “Bid 2.5x for users in canary-456 if the user was added in the last 3 days.”
* Hourly Segment Recency enums do not need to be included if the “Any time less than 1 day” value (enum #7 below) is used.

**Example:**

| targeted_segment | segment_recency | domain | value |
|------------|----------|-------|------------------|
| canary-123 | 1 | espn.com | [expected bid ]|
| canary-456 | 7 | abc.com | 2.5 |
| canary-456 | 8 | abc.com | 2.5 |
| canary-456 | 9 | abc.com | 2.5 |
| ...        | ... | ...             |...  |

| Recency Window | Enum |
|------------|-----------------|
| Less than 15 minutes | 1 |
| Greater than 15 minutes, less than 1 hour | 2 |
| Greater than 1 hour, less than 3 hours | 3 |
| Greater than 3 hours, less than 6 | 4 |
| Greater than 6 hours, less than 12 | 5 |
| Greater than 12 hours, less than 24 | 6 |
| Any time less than 1 day | 7 |
| Greater than 1 day, less than 2 | 8 |
| Greater than 2 days, less than 3 | 9 |
| Greater than 3 days, less than 7 | 10 |
| Greater than 7 days, less than 14 | 11 |
| Greater than 14 days, less than 21 | 12 |
| Greater than 21 days, less than 30 | 13 |

## Frequency
Similar to Segment Recency, the Frequency feature requires two columns in order to be activated. One column specifies the user ID type and frequency count, while the other specifies the frequency look back window.

When using Frequency the user can choose one of several Log Headers, each corresponds to a different type of User ID. This is the user ID that Frequency will be measured from. Only one User ID can be used per Bid Model, for example a model can not contain both standard_freq_count and customer_id_freq_count.

**Log Headers:**
* One of:
  * standard_freq_count
  * ip_address_freq_count
  * customer_id_freq_count
  * liveramp_household_freq_count
  * liveramp_person_freq_count
  * tapad_household_freq_count
  * tapad_person_freq_count
* frequency_window

**Example:**

| standard_freq_count | frequency_window | domain | value |
|------------|--------|---------|------------------|
| 1 | 2 | espn.com | [expected bid ]|
| 4 | 4 | abc.com | [expected bid ]|
| ...        | ... | ...             |...  |


Each of the \*_freq_count and frequency_window values refer to a predefined enumeration.
* \*_freq_count value references a Frequency Count enum.
* frequency_window value refers to a Frequency Window enum.

**Notes:**
* The \*_freq_count  and frequency_window must always be included in a Bid Model together. You cannot include one without the other.
* The frequency_window feature does not support Wild Cards.

**Enumerations:**

| Frequency Count | Enum |
|------------|-----------------|
| 0 | 1 |
| 1 | 2 |
| 2 | 3 |
| 3 | 4 |
| 4-5 | 5 |
| 6-7 | 6 |
| 8+ | 7 |

| Frequency Window | Enum |
|------------|-----------------|
| 1 day | 1 |
| 3 days | 2 |
| 7 days | 3 |
| 14 days | 4 |
| 30 days | 5 |


# FAQ
**Are Wild Cards supported in user based features?**
Yes, except for frequency_window which does not support Wild Cards.

**Are there any changes to how I create prediction files or upload to S3?**
No, the addition of new features does not affect the workflow for creating or uploading new bid models.

**Is there a limit to the size of a Bid Model prediction file?**
Yes, prediction files are limited to 100 MB. However, there is no limit to the number of prediction files that can be uploaded to a single Bid Model.
