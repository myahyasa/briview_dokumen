# REST API Data Delivery explanation Document - BRIview 2023

<a name="readme-top"></a>

# 1. Send Automatic Ticket (Agent Base)

#### HTTP Request
```json
PATCH http://{{host}}:3232/api/tiket
```
#### Preparation
<a name="readme-top"></a>
| Prepared Before Running |  Description  |
| ------------- |:--------------|
|Endpoint Kirim Tiket |/api/tiket|
|Header |Key : Authorization, Value : JWT |
|Body | Json Raw |

#### Requirements Data

| Parameters |  Data Type  | Max Character | 	
| ------------- |:--------------:| -------------|
| no_tiket| String | 255 |
| tid     | String      | 16 |
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

#### Response Description

| Status   |  Description  |
| ------------- |:--------------|
|`200`| OK Everything is working, The resource has been fetched and is transmitted in the message body.|
|`400`| BAD REQUEST The request was invalid or cannot be served. The exact error should be explained in the error payload.|
|`401`| UNAUTHORIZED The request requires user authentication.|
|`404`| NOT FOUND There is no resource behind the URI.|
|`500`| INTERNAL SERVER ERROR API If an error occurs in the global catch blog, the stack trace should be logged and not returned as a response |

#### Result API

| Data |  Description  |
| ------------- |:--------------|
| curl | Json raw |

#### Example API
```json
curl --location --request POST 'http://{{host}}:3232/api/tiket' \
--header 'Authorization: {token}' \
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

# 2. Send Machine Status (Agent Base)

#### HTTP Request
```json
PATCH http://{{host}}:3232/api/status-mesin
```
#### Preparation
<a name="readme-top"></a>
| Prepared Before Running |  Description  |
| ------------- |:--------------|
|Endpoint Kirim Status Mesin |/api/status-mesin|
|Header |Key : Authorization, Value : JWT |
|Body | Json Raw |

#### Requirements Data

| Parameters |  Data Type  | Max Character | 	
| ------------- |:--------------:| -------------|
| tid| String | 255 |
| atm_status    | String      | 255 |
| last_amount   | int   |  64 |
| casette_1_A  | int |  64  |
| casette_2_A | int | 64 |
| casette_3_B    | int  | 64 |
| casette_4_B   | int  | 64 |
| last_transaction   | timestamp  | YYYY-MM-DD HH-MM-SS |

#### Response Description

| Status   |  Description  |
| ------------- |:--------------|
|`200`| OK Everything is working, The resource has been fetched and is transmitted in the message body.|
|`400`| BAD REQUEST The request was invalid or cannot be served. The exact error should be explained in the error payload.|
|`401`| UNAUTHORIZED The request requires user authentication.|
|`404`| NOT FOUND There is no resource behind the URI.|
|`500`| INTERNAL SERVER ERROR API If an error occurs in the global catch blog, the stack trace should be logged and not returned as a response |

#### Result API

| Data |  Description  |
| ------------- |:--------------|
| curl | Json raw |

#### Example API
```json
curl --location --request POST 'http://xxx:3232/api/status-mesin' \
--header 'Authorization: {token}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
      "tid": "002016",
      "atm_status": "IN_SERVICE",
      "last_amount": 1,
      "casette_1_A": 1368,
      "casette_2_A": 1000,
      "casette_3_B": 605,
      "casette_4_B": 100121,
      "last_transaction": "2023-01-06 17:33:15"
    }
  ]'

```
#### Example Response
```json
{
    "draw": 0,
    "recordsTotal": 0,
    "recordsFiltered": 0,
    "status": 200,
    "error": "",
    "message": "OK, Success",
    "data": null
}
```
#### For the ip address and token we will send a website link generate token and ip, to maintain integration privacy security


| Token |  IP |
| ------------- |:--------------|
| XXXXX | http://{{xxx}}:3232/api/status-mesin  |

<!-- CONTACT -->
## Contact

BIT - [@bit](https://twitter.com/bitcorp_id) - corp@bitcorp.id

Project Link : [briview.bitcorp.id](https://github.com/myahyasa/briview_dokumen)

#### Regards. 

Software Developer


[PT BRINGIN INTI TEKNOLOGI][bit]

[bit]:https://bitcorp.id/



<p align="right">(<a href="#readme-top">back to top</a>)</p>


