# Sending Device Location Data to Freckle

## 1. Data Transfer Using The API
This document outlines the communication between 3rd party data vendor and Freckle through Freckle REST API. The endpoints consist of 4 types, generic geolocation-based, beacon enter event, beacon exit event and device triggered visit event.

The Freckle REST API uses the OAuth 2.0 protocol to authorize calls. OAuth is an industry-standard open standard for authorization used by many companies to provide secure access to protected resources.  The following steps are needed to obtain authorization to access Freckle REST API.

1. Register with Freckle (contact your Freckle representative) to obtain a set of credentials (client_id and secret) that you use to authenticate your API calls using the OAuth 2.0 protocol
2. Obtain an access token for your application by sending a request to the Freckle API endpoint using HTTP Basic Auth with your application credentials obtained as described above.  The client_id and secret becomes your user-id and password in HTTP Basic Auth.
3. For all API calls you will need to add the access token in the 'Authorization' header using the syntax defined below.
Note: The Freckle-issued access tokens will expire after 24 hours of inactivity.

### 1.1 All Requests
**Headers for All Requests**
```
Authorization: Bearer <Access-token>      // Auth header to provide api key
```

***Header Notes***
* All fields in the header are required.
* Contact your Freckle representative for authorization API Key.
* HTTP headers are case-insensitive, query string parameters are case-sensitive. 
* Source http://www.w3.org/Protocols/rfc2616/rfc2616-sec4.html#sec4.2 , http://tools.ietf.org/html/rfc7230#section-2.7.3


### 1.2 Endpoints

**Base URL**
```
https://api.freckle.com
```
#### 1.2.1 /geolocation
Endpoint for data vendor to send Freckle geolocation-based data that is not associated with beacon events.  All required fields are indicated in their description.

**Request Method: POST**
```
{
  "device_info": {                // The device information
    "platform": "android|ios",    // *The Device platform (required)
    "idfa": "device identifier",  // *Device Identifier (IDFA or AAID) (required)
    "model": "asus ASUS_Z00TD",   // The model of the device
    "os_version": "21",           // The device's OS version
 },
  "fingerprint": {
    "browser": "com.android.chrome 48.0.2564.95",
    "carrier": "TELUS",
    "device_fingerprint": "asus/WW_Z00T/ASUS_Z00T:5.0.2/LRX22G/release-keys",
    "time_zone": "America/Toronto",
    "user_agent": "Dalvik/2.1.0 (Linux; U; Android 5.0.2; ASUS_Z00TD Build/LRX22G)"
  },
  "location": {                      // The device's location details
    "lat": 43.8772796,               // *Latitude of the device (required)
    "lng": -79.0464828,              // *Longitude of the device (required)
    "time": 1455596905979,           // *Device's time (required)
    "horizontal_accuracy": 28.6,     // *Device's location accuracy from the OS (req)
    "vertical_accuracy": 15.3,       // Device's location accuracy from the OS
    "provider": "gps|network|other", // Device's location provider source
    "bearing": 0,                    // Device's bearing
    "altitude": 0,                   // Device's altitude as reported by the OS
    "speed_ms": 0                    // Device's speed in m/s
  }
}
```

**Response Method: POST**
```
{
  "status": {
    "success": true|false,      // Boolean to success or failure.
    "message": "Some message"   // An optional message related to the response.
  } 
}
```
```
200 Success - Message: OK
401 Unauthorized - Message: Unauthorized
400 Bad Request - Message: <<Field name invalid or missing>>
500 Server Error - Message: Internal Server Error
```


#### 1.2.2 /enter
Endpoint for data vendor to send Freckle beacon enter events.  All required fields are indicated in their description.
**Request Method: POST**
```
{
  "device_info": {                 // The device information
    "platform": "android|ios",     // *The Device platform (required)
    "idfa": "device identifier",   // *Device Identifier (IDFA or AAID) (required)
    "model": "asus ASUS_Z00TD",    // The model of the device
    "os_version": "21",            // The device's OS version
  },
  "beacon": {                        // Beacon info
    "type": "beacon|virtual beacon", // Identify beacon type (optional)                                                
    "uuid": "UUID",
    "major": 20,                     //Beacon major (optional)
    "minor": 20                     // Beacon minor (optional)
  },
  "fingerprint": {
    "browser": "com.android.chrome 48.0.2564.95",
    "carrier": "TELUS",
    "device_fingerprint": "asus/WW_Z00T/ASUS_Z00T:5.0.2/LRX22G//release-keys",
    "time_zone": "America/Toronto",
    "user_agent": "Dalvik/2.1.0 (Linux; U; Android 5.0.2; ASUS_Z00TD Build/LRX22G)"
  },
  "location": {                      // The device's location details
    "lat": 43.8772796,               // *Latitude of the device (required)
    "lng": -79.0464828,              // *Longitude of the device (required)
    "time": 1455596905979,           // *Device's time (required)
    "horizontal_accuracy": 28.6,     // *Device's location accuracy from the OS (req)
    "vertical_accuracy": 15.3,       // Device's location accuracy from the OS
    "provider": "gps|network|other", // Device's location provider source
    "bearing": 0,                    // Device's bearing
    "altitude": 0,                   // Device's altitude as reported by the OS
    "speed_ms": 0                    // Device's speed in m/s
  }
}
```

**Response Method: POST**
```
{
  "status": {
    "success": true|false,      // Boolean to success or failure.
    "message": "Some message"   // An optional message related to the response.
  }
}
```
```
200 Success - Message: OK
401 Unauthorized - Message: Unauthorized
400 Bad Request - Message: <<Field name invalid or missing>>
500 Server Error - Message: Internal Server Error
```

#### 1.2.3 /exit
Endpoint for data vendor to send Freckle beacon exit events.  All required fields are indicated in their description.
**Request Method: POST**
```
{
  "device_info": {                 // The device information
    "platform": "android|ios",     // *The Device platform (required)
    "idfa": "device identifier",   // *Device Identifier (IDFA or AAID) (required)
    "model": "asus ASUS_Z00TD",    // The model of the device
    "os_version": "21",            // The device's OS version
  },
  "beacon": {                        // Beacon info
    "type": "beacon|virtual beacon", // Identify beacon type (optional)                                                
    "uuid": "UUID",
    "major": 20,                    //Beacon major (optional)
    "minor": 20                     //Beacon minor (optional)
  },
  "fingerprint": {
    "browser": "com.android.chrome 48.0.2564.95",
    "carrier": "TELUS",
    "device_fingerprint": "asus/WW_Z00T/ASUS_Z00T:5.0.2/LRX22G//release-keys",
    "time_zone": "America/Toronto",
    "user_agent": "Dalvik/2.1.0 (Linux; U; Android 5.0.2; ASUS_Z00TD Build/LRX22G)"
  },
  "location": {                      // The device's location details
    "lat": 43.8772796,               // *Latitude of the device (required)
    "lng": -79.0464828,              // *Longitude of the device (required)
    "time": 1455596905979,           // *Device's time (required)
    "horizontal_accuracy": 28.6,     // *Device's location accuracy from the OS (req)
    "vertical_accuracy": 15.3,       // Device's location accuracy from the OS
    "provider": "gps|network|other", // Device's location provider source
    "bearing": 0,                    // Device's bearing
    "altitude": 0,                   // Device's altitude as reported by the OS
    "speed_ms": 0                    // Device's speed in m/s
  }
}
```

**Response Method: POST**
```
{
  "status": {
    "success": true|false,      // Boolean to success or failure.
    "message": "Some message"   // An optional message related to the response.
  }
}
```
```
200 Success - Message: OK
401 Unauthorized - Message: Unauthorized
400 Bad Request - Message: <<Field name invalid or missing>>
500 Server Error - Message: Internal Server Error
```

#### 1.2.4 /visit
Endpoint for data vendor to send Freckle device triggered visit events.  All required fields are indicated in their description.

**Request Method: POST**
```
{
  "device_info": {                 // The device information
    "platform": "android|ios",     // *The Device platform (required)
    "idfa": "device identifier",   // *Device Identifier (IDFA or AAID) (required)
    "model": "asus ASUS_Z00TD",    // The model of the device
    "os_version": "21",            // The device's OS version
  },
  "visit": {
    "visit_type": "arrive"|"depart",       // *Required
    "arrival_time": 1455596905979,   // *Time of arrival (required)
    "departure_time": 1455596905979 // *Time of departure (required if type = depart)
  },
  "fingerprint": {
    "browser": "com.android.chrome 48.0.2564.95",
    "carrier": "TELUS",
    "device_fingerprint": "asus/WW_Z00T/ASUS_Z00T:5.0.2/LRX22G//release-keys",
    "time_zone": "America/Toronto",
    "user_agent": "Dalvik/2.1.0 (Linux; U; Android 5.0.2; ASUS_Z00TD Build/LRX22G)"
  },
  "location": {                      // The device's location details
    "lat": 43.8772796,               // *Latitude of the device (required)
    "lng": -79.0464828,              // *Longitude of the device (required)
    "time": 1455596905979,           // *Device's time (required)
    "horizontal_accuracy": 28.6,     // *Device's location accuracy from the OS (req)
    "vertical_accuracy": 15.3,       // Device's location accuracy from the OS
    "provider": "gps|network|other", // Device's location provider source
    "bearing": 0,                    // Device's bearing
    "altitude": 0,                   // Device's altitude as reported by the OS
    "speed_ms": 0                    // Device's speed in m/s
  }
}
```

**Response Method: POST**
```
{
  "status": {
    "success": true|false,      // Boolean to success or failure.
    "message": "Some message"  // An optional message related to the response.
  }
}
```
```
200 Success - Message: OK
401 Unauthorized - Message: Unauthorized
400 Bad Request - Message: <<Field name invalid or missing>>
500 Server Error - Message: Internal Server Error
```

## 2. Data Transfer Using SFTP

### 2.1 Secure FTP Site
Secure FTP credentials will be provided to you by your account representative when your account is created.

### 2.2 Batch Data File Contents
Customer data should NOT contain any information that does not comply with the Freckle IoT privacy policy.

## 2.3 Formatting Your Data

The table below specifies all accepted fields and its format:

|Column|Name|Description|Format|Valid Values/Range|Example|Mandatory|
|---|---|---|---|---|---|---|
1|idfa|unique mobile advertiser ID of the device|string, unhashed|Raw IDFA (iOS) or AAID (Android) value. Input string should be lower cased.|d0798276-abb4-4250-ac08-bb4b2b36ec4e|*
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

If a column is missing data then an empty string needs to be passed for it.

Examples:
```
618075d8-63a5-4b3f-b3c6-a6e9b22b4d86,34.2421234,-124.234245,1439375687000,android,ASUS_Z00TD,21,com.android.chrome 48.0.2564.95,verizon,America/Toronto,Dalvik/2.1.0 (Linux; U; Android 5.0.2; ASUS_Z00TD Build/LRX22G),28.6,15.4,90,120.3,23
48.0.2564.95,verizon,,28.6,15.4,90,120.3,23
48.0.2564.95,verizon,,,,,,
```

### 2.4 Naming Your File
Before uploading your data make sure that you are applying the following formatting rules when generating your files names and folder structure.

```
File Format:          gzip
Filename Prefix:      <year>-<month>-<day>_
Example:              2017-03-14_arbor_data.json.gz

Data Format:          JSON or CSV
Note:                 For CSV please have column name at the first line of each file.

Folder Structure:     <year>/<month>/
example:              2017/03/2017-03-14_arbor_data.json.gz
```

### 2.5 Compression
Files should be compressed using gzip compression in order to save space and time for transfer. Each data file should be compressed individually. A ```.gz``` file suffix component should be added if the file is compressed. 

```
Example: 2017-03-14_arbor_data.json.gz
```

