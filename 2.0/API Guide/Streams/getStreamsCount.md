![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# getStreamsCount



## Definition

Returns the number of **active** streams.





## API Parameter Table

This function has no parameters.





## API Call Template

``` 
getStreamsCount
```



### Success Response in JSON

``` 
{
"data":{
  "streamCount":1
  },
  "description":"Active streams count",
  "status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - ​	streamCount – The number of active streams
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ​
- ​



## Related Links

- Link 1
- Link 2