# Dokumentasi BRIview (Multi Vendor API)

### 1.  POST (Automatic Tiket)

#### HTTP Request
```json
PATCH http://{{host}}:3232/api/tiket
```
#### Response Description

| Status   |  Description  |
| ------------- |:--------------|
|`200`| OK Everything is working, The resource has been fetched and is transmitted in the message body.|
|`201`| CREATED A new resource has been created.|
|`204`| NO CONTENT The resource was successfully deleted, no response body.|
|`400`| BAD REQUEST The request was invalid or cannot be served. The exact error should be explained in the error payload.|
|`401`| UNAUTHORIZED The request requires user authentication.|
|`404`| NOT FOUND There is no resource behind the URI.|
|`500`| INTERNAL SERVER ERROR API If an error occurs in the global catch blog, the stack trace should be logged and not returned as a response |

#### Preparation

| Prepared Before Running |  Description  |
| ------------- |:--------------|
|Endpoint Kirim Tiket |/api/tiket|
|Header |Key : Authorization, Value : JWT |
|Body | Json Raw |

#### Requirements Data

| Parameters |  Data Type  | Max Character | 	
| ------------- |:--------------:| -------------|
| no_tiket| String | 255 |
| tid     | int64      | 12 |
| error   | String    |  255  |
| status  | String |  255  |
| service_level | String | 255 |
| created_at    | String  | 255 |


#### Parameters Send Tiket To Briview

| Parameters    |  Ketentuan Form      | Description  |
| ------------- |:-------------:| -------------|
| no_tiket   | required	  	| `no_tiket` No tiket dari vendor |
| tid         | required      |   Terminal id atau Mesin  	   |
| error         | required      |   Error atau problem mesin yang tampil, Error tersebut harus sesuai dengan service levelnya  	   |
| status         | required      |   Status tiket saat ini, Contoh "OPEN,REQ_CLOSE,DISPATCH,dll" 	   |
| service_level         | required      |   Service level, Contoh "FLM/SLM" 	   |
| created_at         | required      |   Datetime, "2022-12-22 08:58:14"	   |

#### Result API

| Data |  Description  |
| ------------- |:--------------|
| curl | Json raw |

#### Example API
```json
curl --location --request POST 'http://{{host}}:3232/api/tiket' \
--header 'Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2NzI3OTkxMDYsInVzZXIiOnsiaWQiOjI1fX0.tPBNCEXELWvCFl9_SjyskCCXlqwyJqBLix7Cm3WKf6g' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "no_tiket": "A2022122216000212",
        "tid": "160002",
        "error": "PRINTER ERROR",
        "status": "OPEN",
        "service_level": "FLM",
        "created_at": "2022-12-22 08:58:14"
    }
]'

```
#### Example Response
```json
{
    "status": 200,
    "message": "OK",
    "data": [
        {
            "no_tiket": "A2022122216000212",
            "tid": "160002",
            "error": "PRINTER ERROR",
            "status": "OPEN",
            "service_level": "FLM",
            "created_at": "2022-12-22 08:58:14"
        }
    ]
}
```
#### For the ip address and token we will send a website link generate token and ip, to maintain integration privacy security


| Token |  IP |
| ------------- |:--------------|
| XXXXX | http://{{xxx}}:3232/api/tiket  |


#### Regards. 

Software Developer


#### PT BRINGIN INTI TEKNOLOGI
