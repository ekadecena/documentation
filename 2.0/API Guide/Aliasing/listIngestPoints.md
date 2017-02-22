![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# listIngestPoints



## Definition

Lists the currently available Ingest Points.





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listIngestPoints
```



### Success Response in JSON

``` 
{
"data":{
    "privateStreamName":"testIngestPoint",
    "publicStreamName":"testPublicStreamName"
},
"description":"Available ingest points",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– List of pairs
  - privateStreamName –The private stream name which was set
  - publicStreamName – The public stream name which was set
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasIngestPoints** in config.lua should be **TRUE**
- ​





## **Related Links**

- Link 1
- Link 2