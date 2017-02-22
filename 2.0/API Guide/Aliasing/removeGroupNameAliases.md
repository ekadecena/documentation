![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# removeGroupNameAliases



## Definition

This command will remove the group name given the alias name.





## API Parameter Table



| Parameter Name |  Type  | Mandatory | Default Value | Description                             |
| :------------: | :----: | :-------: | :-----------: | --------------------------------------- |
|   aliasName    | string |   true    |    *null*     | The alias alternative to the group name |



## API Call Template

``` 
removeGroupNameAlias aliasName=<groupAliasName>
```



### Sample API Call

``` 
removeGroupNameAlias aliasName=testGroupAlias
```



### Success Response in JSON

``` 
{
"data":[
    {
    "aliasName":"testGroupAlias",
    "groupName":"testAliasGroupName"
}
],
"description":"Group Alias removed",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– Provides the following information for each group name alias
  - aliasName – The alias alternative to the `groupname`
  - groupName – The original group name
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- **hasStreamAliases** in config.lua should be **TRUE**
- ​





## **Related Links**

- Link 1
- Link 2