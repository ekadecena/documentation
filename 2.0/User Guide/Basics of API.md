# EMS API Explorer



## Basics of API

### A. Streams API

- #### pullStream

  The EMS provides an extremely robust platform for stream protocol re-encapsulation. That is, the EMS will allow the translation from one streaming protocol to another protocol, allowing the reach to a wide range of video/audio clients, regardless of how the video/audio source is configured.

  The first step to achieve protocol re-encapsulation is to get the original stream into the EMS. The most common method for doing this is by using the “**Pull a Stream**” mechanism, but other systems can also push a stream into the EMS.

  The `pullStream` API provides a way to tell the EMS to retrieve an existing stream.

  Below are the examples of how to pull a stream in different formats:

  **a. pulling an RTMP stream**

  ```
  pullStream uri=rtmp://<STREAM_ADDRESS> localStreamName=RTMPTest
  ```

  **b. pulling an RTSP stream**

  ```
  pullStream uri=rtsp://<STREAM_ADDRESS> localStreamName=RTSPTest

  ```

  **c. pulling an RTP - UDP stream**

  ```
  pullStream uri=rtp://<STREAM_ADDRESS> localStreamName=RTPTest isAudio=0 spsBytes=Z0LAHpZiA2P8vCAAAAMAIAAABgHixck= ppsBytes=aMuMsg==

  ```

  **d. pulling an MPEG-TS stream**

  - For **UDP MPEG-TS** streams, use:

  ```
  pullStream uri=dmpegtsudp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest

  ```

  This can be used for multicast streams as well. If the address of the stream is in the IP Multicast range, the EMS will automatically join the multicast group so that it can pull the stream.

  - For **TCP MPEG-TS** streams, use:

  ```
  pullStream uri=dmpegtstcp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest

  ```

  **Note:**

  The “**d**” in front of mpegts ( **d**mpegts) in the URIs above refers to “deep parsing”. Using the URI, the inbound MPEG-TS stream can be re-encapsulated into other protocols such RTMP or RTSP. If the only output format will be MPEG-TS (e.g. EMS is used as an MPEG-TS pass-through), then mpegtsudp and mpegtstcp can be used as the URI protocol specifier. This will speed the transfer of the MPEG-TS streams since no parsing will occur.

  **e. pulling a LOCAL SDP FILE**

  EMS is also capable in pulling an Session Description Protocol (SDP) file. An SDP is a format for describing the initialization parameters of streaming media sessions. SDP does not deliver media itself but is used for negotiation between end points of media type, format, and all associated properties.

  ```
  pullStream uri=file://<FILEPATH>/FILENAME.sdp localStreamName=sdpFileTest

  ```

  **Note:**

  The SDP must reside in the file system accessible by EMS.

  ​

  ​

- #### pushStream

  EMS is capable of receiving streams that are pushed to it from other servers. An RTMP listener is available on port **1935** , an RTSP listener on **5544** and a LiveFLV listener on port **6666**.

  Steps on how to do the actual stream push needs to be consulted with the stream source, as every system has different ways of accomplishing this.

  General format of **pushStream** command in EMS:

  **a. pushing an RTMP stream**

  ```
  pushStream uri=rtmp://DestinationAddress localStreamName=SomeLocalStreamName
  ```

  **b. pushing an RTSP stream**

  ```
  pushStream uri=rtsp://DestinationAddress:port localStreamName=SomeLocalStreamName
  ```

  **c. pushing an MPEG-TS stream**

  MPEG-TS streams, in general, don’t have the concept of a stream identifier (name). The EMS will assign a name to an inbound MPEG-TS stream for internal uses, but outside of the EMS, that name is not used. To obtain an MPEG-TS stream from the EMS, it must be first pushed out to the network.

  Sample commands to do this are:

  ```
  pushStream uri=mpegtsudp://DestinationAddr localStreamName=SomeLocalStream
  ```

  or

  ```
  pushStream uri=mpegtstcp://DestinationAddr localStreamName=SomeStream
  ```

  If the UDP destination address is in the multicast range, the pushed stream will be a multicast stream.

  ​

  **d. Push-In Authentication**

  For security, EMS has an option to require all streams which are pushed into the server be authenticated using authentication details that are specified in `config.lua` and `users.lua`. By default, the authentication configuration is **disabled**.

  To enable authentication in the EMS the following should be set:

  1. Set the boolean value in `auth.xml` to true

     ```
      <BOOL name="">true</BOOL>
     ```

  2. Remove comments (`--[[` .. `]]--`) in authentication in `config.lua` 

     ```
      --[[ //remove
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
          --authenticatePlay=false,
        }
      },  
      ]]-- //remove
     ```

  ​

  ​	**d.1.Play authentication**

  ​	The `authenticatePlay` functionality works only with RTSP sources. If set to **true**, it will prompt for a username and password window when stream is requested for playback.

  ​	**Add users in users.lua**

  ​	The configurations in the `users.lua` will serve as the username and password that needs to be inputted in the authentication window if `authenticatePlay` is set to true.

  ```
  users=
  {
    USER_A="12345678",
  }
  realms=
  {
    {
      name="EVOSTREAM stream router",
      method="Digest",
      users={
        "USER_A",
      },
    },
  }
  ```

  **Note:** Multiple users may add in this section. Just add entries under each user entry.

  ```
  users=
  {
    USER_A="12345678",
    USER_B="87654321",
  }
  realms=
  {
    {
      name="EVOSTREAM stream router",
      method="Digest",
      users={
        "USER_A",
        "USER_B",
      },
    },
  }
  ```

------



