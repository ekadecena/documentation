![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# getConfigInfo



## Definition

Returns the information of the stream by the configId.





## API Parameter Table



| Parameter Name |  Type   | Mandatory | Default Value | Description                              |
| :------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|       id       | integer |   true    |    *null*     | The `configId` of the configuration to get some information |

## API Call Template

``` 
getConfigInfo id=<configId>
```



### Sample API Call

``` 
getConfigInfo id=1
```



### Success Response in JSON

``` 
{
"data":{
	"audioCodecBytes":"",
	"configId":1,
	"emulateUserAgent":"EvoStream Media Server (www.evostream.com) player",
	"forceTcp":false,
	"httpProxy":"",
	"httpStreamType":"ts",
	"isAudio":true,
	"keepAlive":true,
	"localStreamName":"testpullStream",
	"operationType":1,
	"pageUrl":"",
	"ppsBytes":"",
	"rangeEnd":-1,
	"rangeStart":-2,
	"rtcpDetectionInterval":10,
	"sendRenewStream":false,
	"spsBytes":"",
	"ssmIp":"",
	"status":{
	"current":{
	"code":0,
	"description":"Streaming",
	"timestamp":1475482701,
	"uniqueStreamId":1
	},
	"previous":{
		"code":3,
		"description":"Connected",
		"timestamp":1475482700,
		"uniqueStreamId":0
		}
	},
	"swfUrl":"",
	"tcUrl":"",
	"tos":256,
	"ttl":256,
	"uri":"rtmp:\/\/s2pchzxmtymn2k.cloudfront.net\/cfx\/st\/mp4:sintel.mp4"
},
"description":"Configuration Info",
"status":"SUCCESS"
}
```



#### **JSON Response**

The JSON response contains the following details:

- data – The information about the configuration


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ​
- ​





## **Related Links**

- Link 1
- Link 2