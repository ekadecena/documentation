![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# setAuthentication



## Definition

Will enable/disable RTMP authentication.





## API Parameter Table

| Parameter Name |  Type   | Mandatory | Default Value | Description                              |
| :------------: | :-----: | :-------: | :-----------: | ---------------------------------------- |
|    enabled     | boolean |   true    |    *null*     | **1** to enable, **0** to disable authentication |



## API Call Template

``` 
setAuthentication enabled=1
```



### Success Response in JSON

``` 
{
"data":{
    "enabled":true
},
"description":"Authentication mode updated",
"status":"SUCCESS"
}
```



#### **JSON Response**

The JSON response contains the following details:

- data – The data to parse
  - enabled – **true** if authentication is enabled, **false** if not


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

### Notes

- ​

- ​





## **Related Links**

- Link 1
- Link 2