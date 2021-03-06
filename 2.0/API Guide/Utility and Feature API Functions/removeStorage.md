![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# removeStorage



## Definition

This function removes a storage location.





## API Parameter Table

| Parameter Name |  Type  | Mandatory | Default Value | Description                  |
| :------------: | :----: | :-------: | :-----------: | ---------------------------- |
|  mediaFolder   | string |   true    |    *null*     | The path to the media folder |



## API Call Template

``` 
removeStorage mediaFolder=<targetFolderPath>
```



### Sample API Call

``` 
removeStorage mediaFolder=C:\EvoStream\testMediaFolder
```



### Success Response in JSON

``` 
{
"data":{
    "clientSideBuffer":15,
    "description":"TestStorage",
    "enableStats":true,
    "externalSeekGenerator":true,
    "keyframeSeek":true,
    "maxPlaylistFileSize":4096,
    "mediaFolder":"C:\\EvoStream\\testMediaFolder\\",
    "metaFolder":"C:\\EvoStream\\testMediaFolder\\",
    "name":"anotherMediaFolder",
    "seek Granularity":300000
},
"description":"Storage removed",
"status":"SUCCESS"
```



#### **JSON Response**

The JSON response contains the following details:

- data – The data to parse
  - clientSideBuffer – How much data should be maintained on the client side when a file is played from this storage
  - description – Description given to this storage. Used to better identify the storage
  - enableStats – If **true**, *.stats files are going to be generated once the media files are used
  - externalSeekGenerator – If **true**, *.seek and *.meta files are going to be generated by another external tool
  - keyframeSeek – If **true**, the seek/meta files are going to be generated having only keyframe seek points
  - maxPlaylistFileSize - 
  - mediaFolder – The path to the media folder
  - metaFolder – Path to the folder which is going to contain all the seek/meta files. If missing, the seek/meta files are going to be generated inside the media folder
  - name – Name given to this storage. Used to better identify the storage
  - seekGranularity – Sets the granularity for the seek files


- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

### Notes

- ​

- ​





## **Related Links**

- Link 1
- Link 2