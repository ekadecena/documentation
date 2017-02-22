![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# flushGroupNameAliases



## Definition

This command invalidates all group name aliases.





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
flushGroupNameAliases
```



### Success Response in JSON

``` 
{
"data":null,
"description":"All group name aliases are flushed",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– Nothing to parse for this command
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasIngestPoints** in config.lua should be **TRUE**
- ​





## **Related Links**

- Link 1
- Link 2