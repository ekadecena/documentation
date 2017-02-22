![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# listInboundStreamNames



## Definition

Provides a list of all the current inbound `localStreamNames`.





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listInboundStreamNames
```



### Success Response in JSON

``` 
{
"data":[
  {
  "name":"teststream1"
  },
  {
  "name":"teststream2"
  },
  {
  "name":"teststream3"
  }
],
"description":"Inbound local stream names",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.
  - name - the `localStreamName` of the inbound stream
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ​
- ​





## **Related Links**

- Link 1
- Link 2