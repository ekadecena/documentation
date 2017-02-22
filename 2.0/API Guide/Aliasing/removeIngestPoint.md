![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# removeIngestPoint



## Definition

Removes an RTMP ingest point.





## API Parameter Table

|  Parameter Name   |  Type  | Mandatory | Default Value | Description                              |
| :---------------: | :----: | :-------: | :-----------: | ---------------------------------------- |
| privateStreamName | string |   true    |    *null*     | The Ingest Point that will be deleted identified by the `privateStreamName` |



## API Call Template

``` 
removeIngestPoint privateStreamName=<theIngestPoint>
```



### Sample API Call

``` 
removeIngestPoint privateStreamName=testIngestPoint
```

### Success Response in JSON

``` 
{
"data":{
    "privateStreamName":"testIngestPoint",
    "publicStreamName":"testPublicStreamName"
},
"description":"Ingest point removed",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - privateStreamName – The `privateStreamName` of the deleted Ingest Point
  - publicStreamName – The `publicStreamName` of the deleted Ingest Point
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasIngestPoint** is config.lua should be set to **TRUE**
- ​
- ​





## **Related Links**

- Link 1
- Link 2