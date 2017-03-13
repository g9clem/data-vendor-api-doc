##Data Processing

###Secure FTP Site
Secure FTP credentials will be provided to you by your account representative when your account is created.

###Batch Data File Contents
Customer data should NOT contain any information that does not comply with the Freckle IoT privacy policy.

###File Format
Mobile location data must be formatted as text files, with one line per record and Tab characters delimited fields. Character encoding should be UTF-8. Lines should be terminated with the newline character (0xA). Carriage return characters (0xD) are permitted and can act as part of the line termination.
The delimiter between the columns is comma (,). If a column can have multiple valid values, those values need to be delimited by a comma.

Recommended Device ID format is raw and un-hashed. If hashed values are provided, hashing algorithm must be either MD5 or SHA-1.

To maximize data accuracy, each record must contain the following:
*Unique Mobile Advertising ID, which represents the device and persists across files. For iOS this is the IDFA, for Android it is the AAID.
*Geo data such as lat, long, horizontal accuracy, and timestamp of the event.

The table below specifies all accepted fields and its format:


|Column|Name|Description|Format|Valid Values/Range|Example|Mandatory|
|---|---|---|---|---|---|---|
1|idfa|unique mobile advertiser ID of the device|string, unhashed|Raw IDFA (iOS) or AAID (Android) value.|Input string should be lower cased.|d0798276-abb4-4250-ac08-bb4b2b36ec4e|*
2|lat|latitiude of the device|signed decimal number|[-90.0, 90.0]|43.8772796|*
3|lng|longitude of the device|signed decimal number|[-180.0, 180.0]|-79.0464828|*
4|time|epoch time of the event|unsigned integer number|[0, 2147483647000]|1455596905979|*
5|platform|device OS type|string|Android, iOS|android, ios
6|model|device model|string|asus ASUS_Z00TD
7|os_version|device's operating system version|string|21
8|browser|device's browser|string|com.android.chrome 48.0.2564.95
9|carrier|device's wireless carrier|string|verizon
10|time_zone|device's time zone|string|America/Toronto
11|user_agent|device's user agent|string|Dalvik/2.1.0 (Linux; U; Android 5.0.2; ASUS_Z00TD Build/LRX22G)
12|horizontal_accuracy|horizontal location accuracy from the device|unsigned decimal number|28.6
13|vertical_accuracy|vertical location accuracy from the device|unsigned decimal number|15.4
14|bearing|device's compass bearing|signed decimal number|[-180.0, 180.0]|90
15|altitude|device's altitude |unsigned decimal number|120.3
16|speed_ms|device's speed in meters per second|unsigned decimal number |23

