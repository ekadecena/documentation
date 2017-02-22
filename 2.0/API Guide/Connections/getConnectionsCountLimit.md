![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# getConnectionsCountLimit



## Definition

Returns the limit of concurrent connections. This is the maximum number of connections an EMS instance will allow at one time.





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
getConnectionsCountLimit
```



### Success Response in JSON

``` 
{
"data":{
    “cuurent”:3
    "limit":0
},
"description":"Connection counters",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse
  - current – The current number of concurrent connections
  - limit – The maximum number of concurrent connections
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ​
- ​





## **Related Links**

- Link 1
- Link 2