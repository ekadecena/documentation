![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# isStreamRunning



## Definition

Checks a specific stream if it is running or not.





## API Parameter Table



| Parameter Name  |  Type   | Mandatory | Default Value | Description                           |
| :-------------: | :-----: | :-------: | :-----------: | ------------------------------------- |
|       id        | integer |   true    |    *null*     | The unique id of the stream to check. |
| localStreamName | string  |   true    |    *null*     | The name of the stream to check.      |

## API Call Template

``` 
isStreamRunning id=<configId>
```

OR

``` 
isStreamRunning localStreamName=<localStreamName>
```



### Sample API Call

``` 
isStreamRunning localStreamName=testpullStream
```



### Success Response in JSON

``` 
"data":{
	"Running":true
},
"description":"Stream status:",
"status":"SUCCESS"
```

``` 
"data":{
	"Running":false
},
"description":"Stream status:",
"status":"SUCCESS"
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - configId – The identifier for the pullPushConfig.xml entry
  - Other fields present are dependent on stream type
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- Either add the parameter id or localStreamName in the API call
- ​





## **Related Links**

- Link 1
- Link 2