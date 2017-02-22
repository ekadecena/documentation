![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# removeStreamAlias



## Definition

Removes an alias of a stream.





## API Parameter Table

| Parameter Name |  Type  | Mandatory | Default Value | Description         |
| :------------: | :----: | :-------: | :-----------: | ------------------- |
|   aliasName    | string |   true    |    *null*     | The alias to delete |



## API Call Template

``` 
removeStreamAlias aliasName=<aliasName>
```



### Sample API Call

``` 
removeStreamAlias aliasName=testAlias
```

### Success Response in JSON

``` 
{
"data":{
	"aliasName":"testAlias"
},
"description":"Alias removed",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse
  - ​	aliasName – The alias of the stream that was removed
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasStreamAliases** in config.lua should be **TRUE**
- ​





## **Related Links**

- Link 1
- Link 2