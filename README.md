# Dokumentasi BRIVIEW (Multi Vendor API)

### 1.  Send Tiket

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
|Endpoint History Tiket |/api/tiket-log|
|Header |Key : Authorization, Value : JWT |
|Body | Json Raw |


#### Parameters Send Tiket To Briview

| Parameters    |  Ketentuan Form      | Description  |
| ------------- |:-------------:| -------------|
| no_tiket   | required	  	| `no_tiket` No tiket dari vendor |
| tid         | required      |   Terminal id atau mesin  	   |
| error         | required      |   Error atau problem mesin yang tampil, error tersebut harus sesuai dengan service levelnya  	   |
| status         | required      |   Status tiket saat ini, contoh OPEN,REQ_CLOSE,DISPATCH,dll 	   |
| service_level         | required      |   Service level, contoh FLM/SLM 	   |
| remarks_bri         | optional      |   Remarks yang diberikan oleh bri untuk vendor 	   |
| remarks_vendor         | optional      |   Remarks yang diberikan oleh vendor untuk bri	   |
| image         | optional      |   Path image yang didapatkan setelah hit endpoint upload image	   |

#### Result API

| Data |  Description  |
| ------------- |:--------------|
| curl | Json raw |

#### Example API
```json
curl --location --request POST 'http://34.124.128.222:3232/api/tiket' \
--header 'Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2NzI3OTkxMDYsInVzZXIiOnsiaWQiOjI1fX0.tPBNCEXELWvCFl9_SjyskCCXlqwyJqBLix7Cm3WKf6g' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "no_tiket": "A2022122216000212",
        "tid": "160002",
        "error": "VANDALISM",
        "status": "OPEN",
        "service_level": "FLM",
        "remarks_bri": "TESTING",
        "remarks_vendor": "TESTING",
        "image": "/testing/imageTiketVendor/A20220422213025153861023.png",
        "nama_spv": "Joko",
        "nama_eng": "Widodo",
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
            "error": "VANDALISM",
            "status": "OPEN",
            "service_level": "FLM",
            "remarks_bri": "TESTING",
            "remarks_vendor": "TESTING",
            "image": "/testing/imageTiketVendor/A20220422213025153861023.png",
            "nama_spv": "Joko",
            "nama_eng": "Widodo",
            "created_at": "2022-12-22 08:58:14"
        }
    ]
}
```
### 2. Get History Tiket  

#### HTTP Request
```json
PATCH http://{{host}}:3232/api/tiket-log
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

#### Parameters Get History Tiket by Filter

| Parameters    |    Ketentuan Form   | Description  |
| ------------- |:-------------:| -------------|
| no_tiket   | optional  	| `no_tiket` Nomer Tiket|
| created_at    | optional    |   terminal id atau mesin  	   |
| date         | optional      |   error atau problem mesin yang tampil, error tersebut harus sesuai dengan service levelnya  	   |


#### Result API

| Data |  Description  |
| ------------- |:--------------|
| curl | Json raw |

#### Example API
```json
curl --location --request POST 'http://34.124.128.222:3232/api/tiket-log' \
--header 'Authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2NzI3OTkxMDYsInVzZXIiOnsiaWQiOjI1fX0.tPBNCEXELWvCFl9_SjyskCCXlqwyJqBLix7Cm3WKf6g' \
--form 'no_tiket="TESTINGG 4"' \
--form 'created_at="2022-12-22 07:58:14"' \
--form 'date="2022-12-22"'
```
#### Example Response
```json
{
    "recordsTotal" : "413",
    "recordsFiltered" : "1",
    "status":"200",
    "massage":"data ditemukan",
	"data": [
    {
      "id": 464,
      "multi_vendor_id": "TESTINGG 4", //the data you are looking for
      "tb_master_vendor_id": 72,
      "tb_tid_allocation_id": 3407,
      "tb_atm_error_vendor_id": 0,
      "tb_status_id": 2,
      "tb_service_level_id": 1,
      "remarks_bri": "TESTING",
      "remarks_vendor": "TESTING",
      "image": "/testing/imageTiketVendor/A20220422213025153861023.png",
      "nama_spv": "TEST",
      "nama_eng": "TEST",
      "created_at": "2022-12-22 07:58:14" //the data you are looking for
    }
  ]
}
```
