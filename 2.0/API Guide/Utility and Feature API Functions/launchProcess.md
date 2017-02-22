![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# launchProcess



## Definition

Allows the user to launch an external process on the local machine. This can be used to do transcoding when paired with applications such as LibAVConv and FFMPEG.





## API Parameter Table



| Parameter Name |  Type   | Mandatory |              Default Value               | Description                              |
| :------------: | :-----: | :-------: | :--------------------------------------: | ---------------------------------------- |
| fullBinaryPath | string  |   true    |                  *null*                  | The path to the executable               |
|   keepAlive    | boolean |   false   |                 1 *true*                 | If the process dies for any reason, the EMS will restart the external application when `keepAlive` is 1 |
|   arguments    | string  |   false   |           *zero-length string*           | Complete list of arguments that need to be passed to the process, delimited by ESCAPED SPACES (“\ “) |
|   groupName    | string  |   false   | *if not assigned, will create a random value process_group_xxx* | The group name assigned to the process   |
| $[ENV]=[VALUE] | string  |   false   |           *zero-length string*           | Any number of environment variables that need to be set just before launching the process |



## API Call Template

``` 
launchProcess parameterA=<value> parameterB=<value> ...
```



### Sample API Call

``` 
launchProcess fullBinaryPath=/home/ems/ffmpeg_preset.sh arguments=10fps\ Stream1\ Stream1_10fps keepAlive=1 $SAMPLE_E_VAR=MyVal
```

This sample command launches a script, named ffmpeg_prest.sh, which presumably contains a shell-script that will run FFMPEG with a specific set of parameters.

The arguments field passes the three values (“10fps”, “Stream1”, “Stream1_10fps”) to the ffmpeg_preset.sh script. In this example, these parameters might tell this hypothetical script to transcode Stream1 to be only 10 frames-per-second, and then name the resultant stream “Stream1_10fps”.

The final parameter is an example for setting an environment variable (SAMPLE_E_VAR set to MyVal) on the command line prior to script/binary execution.



### Success Response in JSON

``` 
{
"data":{
    "configId":2,
    "ersip":"52.6.14.61",
    "ersport":3535,
    "keepAlive":true,
    "name":"evostreamms",
    "operationType":9,
    "roomid":"testRoom",
    "sslCert":"..\/config\/server.cert",
    "sslKey":"..\/config\/server.key"
},
"description":"Started WebRTC Negotiation Service",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data – The data to parse.
  - configId - The configuration ID for this command
  - ersip – The IP address of the ERS
  - ersport – The port of the ERS
  - keepAlive - ??
  - name - ??
  - operationType – The type of operation
  - roomId – The room identifier
  - sslCert - The SSL certificate
  - sslKey - The SSL key certificate
- description – Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- Room ID can only be started once
- ​





## **Related Links**

- Link 1
- Link 2