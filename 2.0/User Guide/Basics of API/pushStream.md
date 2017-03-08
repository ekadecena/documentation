[TOC]

# pushStream

EMS is capable of receiving streams that are pushed to it from other servers. An RTMP listener is available on port **1935** , an RTSP listener on **5544** and a LiveFLV listener on port **6666**.

Steps on how to do the actual stream push needs to be consulted with the stream source, as every system has different ways of accomplishing this.



## How To

Below are the examples of how to push a stream in different formats:

### RTMP stream

```
pushStream uri=rtmp://DestinationAddress localStreamName=SomeLocalStreamName
```



### RTSP stream

```
pushStream uri=rtsp://DestinationAddress:port localStreamName=SomeLocalStreamName
```



### MPEG-TS stream

MPEG-TS streams, in general, donâ€™t have the concept of a stream identifier (name). The EMS will assign a name to an inbound MPEG-TS stream for internal uses, but outside of the EMS, that name is not used. To obtain an MPEG-TS stream from the EMS, it must be first pushed out to the network.

Sample commands to do this are:

```
pushStream uri=mpegtsudp://DestinationAddr localStreamName=SomeLocalStream
```

or

```
pushStream uri=mpegtstcp://DestinationAddr localStreamName=SomeStream
```



### Push-In Authentication

For security, EMS has an option to require all streams which are pushed into the server be authenticated using authentication details that are specified in `config.lua` and `users.lua`. By default, the authentication configuration is disabled.

To enable authentication in the EMS the following should be set:

1. Set [auth.xml]() to true

   ```
   <BOOL name="">true</BOOL>
   ```

2. Remove comments (`--[[` .. `]]--`) and configure authentication in `config.lua`

   ```
   authentication=
    {
      rtmp=
      {
        type="adobe",
        encoderAgents=
      {
        "FMLE/3.0 (compatible; FMSc/1.0)",
        "Wirecast/FM 1.0 (compatible; FMSc/1.0)",
        "EvoStream Media Server (www.evostream.com)"
      },
        usersFile="..\\config\\users.lua"
      },
      rtsp=
      {
        usersFile="..\\config\\users.lua",
        authenticatePlay=true,
      }
    },
   ```

3. Add user in [users.lua]()

   ```
   users=
   {
   	evo="evo123",
   	stream="stream123",
   }

   realms=
   {
   	{
   		name="EVOSTREAM stream router",
   		method="Digest",
   		users={
   			"evo",
   			"stream",
   		},
   	},
   }
   ```

4. Run EMS and send the `pushStream` command





## JSON CLI Response

**API Call:**

```
pushStream uri=rtmp://192.168.2.105/live localStreamName=testpullstream targetStreamName=testpushstream 
```

**JSON Response:**

```
Command entered successfully!
Local stream testpullstream enqueued for pushing to rtmp://192.168.2.105/live as
 testpushstream

    configId: 2
    forceTcp: false
    keepAlive: true
    localStreamName: testpullstream
    targetStreamName: testpushstream
    targetStreamType: live
    targetUri:
      fullUri: rtmp://192.168.2.105/live
      port: 1935
      scheme: rtmp
```


## Playing a Pushed Steam

Playing a pushed stream is similar in playing a pulled stream. 

The basic commands in playing a pushed stream in EMS are the following:

- **RTMP**

  The format of the RTMP URI is as follows:

  ```
  rtmp[t|s]://[username[:password]@]ip[:port]/<appName>/<stream_name>
  ```

  As an example, to play an RTMP stream, use the following URI in the Flash enabled player:

  ```
  rtmp://<EMS_IP_ADDRESS>/live/localStreamName
  ```

- **RTMP**

  The format of the RTSP URI is as follows:

  ```
  rtsp://[username[:password]@]ip[:port]/[ts|vod|vodts]/<stream_name or MP4 file name>
  ```

  **Note:**

  The command is very similar to RTMP, except for the absence of the “appName” field.

  As an example, to play an RTSP stream, the following URI in an RTSP enabled player can be used:

  ```
  rtsp://<EMS_IP_ADDRESS>:5544/localStreamName
  ```

  By default, the EMS will send the video/audio payload data via RTP. If MPEG-TS is needed instead, simply specify it in the request URI: