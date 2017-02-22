![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# listInboundStreams



## Definition

Provides a complete detailed list of all the current inbound `localStreamNames`.





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
listInboundStreams
```



### Success Response in JSON

``` 
{
"data":[
  {
  "appName":"evostreamms",
  "audio":{
    "bytesCount":0,
    "codec":"AAAC",
    "codecNumeric":4702111241970122752,
    "droppedBytesCount":0,
    "droppedPacketsCount":0,
    "packetsCount":0
    },
  "bandwidth":512,
  "connectionType":0,
  "creationTimestamp":1462950774977.0740,
  "edgePid":0,
  "farIp":"127.0.0.1",
  "farPort":36968,
  "ip":"127.0.0.1",
  "name":"teststream",
  "nearIp":"127.0.0.1",
  "nearPort":5544,
  "outStreamsUniqueIds":[
    67
    ],
  "port":5544,
  "processId":5785,
  "processType":"origin",
  "queryTimestamp":1462950861518.4170,
  "type":"IFP",
  "typeNumeric":5279995574068707328,
  "uniqueId":66,
  "upTime":86541.3430,
  "userAgent":"EvoStream Media Server (www.evostream.com)",
  "video":{
    "bytesCount":0,
    "codec":"VH264",
    "codecNumeric":6217274493967007744,
    "droppedBytesCount":0,
    "droppedPacketsCount":0,
    "height":240,
    "level":30,
    "packetsCount":0,
    "profile":66,
    "width":424
  }
  },
],
"description":"Available inbound streams",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data –  The data to parse.

  - appName - EvoStream Media Server

  - audio – stats about the audio portion of the stream

    - bytesCount – Total amount of audio data received
    - codec - 
    - codecNumeric - 
    - droppedBytesCount - The number of video bytes lost
    - droppedBytesCount – The number of audio bytes lost
    - droppedPacketsCount – The number of lost audio packets
    - packetsCount – Total number of audio packets received

  - bandwidth – The current bandwidth utilization of the stream

  - connectionType - 

  - canDropFrames – *Outstreams only*. Flag set by client allowing for dropped frames/packets

  - creationTimestamp – The UNIX timestamp for when the stream was created. UNIX time is expressed as the number of seconds since the UNIX Epoch (Jan 1, 1970)

  - edgePid – Internal flag used for clustering

  - farIp - The IP address of the distant party

  - farPort - The port used by the distant party

  - ip - IP address of the source stream’s host

  - inStreamUniqueID – *For pushed streams.* The id of the source stream.

  - name – the `localStreamName` for this stream

  - nearIp - The IP address used by the local computer

  - nearPort - The port used by the local computer

  - outStreamsUniqueIDs – *For pulled streams.* An array of the “out” stream IDs associated with this “in” stream

  - pageUrl - A link to the page that originated the request (often unused)

  - port - The port bound to the service

  - processId - 

  - processType - 

  - queryTimestamp – The time (in UNIX seconds) when the information in this request was populated

  - type – The type of stream this is. The first two characters are of most interest:

    - char 1 = I for inbound, O for outbound

    - char 2 = N for network, F for file

    - char 3+ = further details about stream

      example: INR = Inbound Network Stream (a stream coming from the network into the EMS)

  - typeNumeric - ??

  - uniqueId – The unique ID of the stream

  - uptime – The time in seconds that the stream has been alive/running for

  - userAgent - ??

  - video – Stats about the video portion of the stream

    - bytesCount – Total amount of video data received
    - codec - ??
    - codecNumeric - ??
    - droppedBytesCount – The number of video bytes lost
    - droppedPacketsCount – The number of lost video packets
    - height – The video stream’s pixel height
    - level - ??
    - packetsCount – Total number of video packets received
    - profile - ??
    - width - The video stream’s pixel width

- description– Describes the result of parsing/executing the command

- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ​
- ​





## **Related Links**

- Link 1
- Link 2