![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# getConnectionsCount



## Definition

Returns the number of active connections.  This includes connections necessary for EMS operations (telnet, license manager, interface, etc.) and all connections opened by streams (RTSP-UDP-RTP ports).





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
getConnectionsCount
```



### Success Response in JSON

``` 
{
"data":{
    "count":3
},
"description":"Active connections count",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse
  - count – The number of active connections
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ​
- ​





## **Related Links**

- Link 1
- Link 2