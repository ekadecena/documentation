# pushStream



## Definition

The EMS provides an extremely robust platform for stream protocol re-encapsulation. That is, the EMS will allow the translation from one streaming protocol to another protocol, allowing the reach to a wide range of video/audio clients, regardless of how the video/audio source is configured.

The first step to achieve protocol re-encapsulation is to get the original stream into the EMS. The most common method for doing this is by using the “**Pull a Stream**” mechanism, but other systems can also push a stream into the EMS.

The `pullStream` API provides a way to tell the EMS to retrieve an existing stream.



## How To

Below are the examples of how to pull a stream in different formats:

### RTMP stream

```
pullStream uri=rtmp://<STREAM_ADDRESS> localStreamName=RTMPTest
```



### RTSP stream

```
pullStream uri=rtsp://<STREAM_ADDRESS> localStreamName=RTSPTest
```



### RTP - UDP stream

```
pullStream uri=rtp://<STREAM_ADDRESS> localStreamName=RTPTest isAudio=0 spsBytes=Z0LAHpZiA2P8vCAAAAMAIAAABgHixck= ppsBytes=aMuMsg==
```



### MPEG-TS stream

#### UDP MPEG-TS stream

```
pullStream uri=dmpegtsudp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest
```

This can be used for multicast streams as well. If the address of the stream is in the IP Multicast range, the EMS will automatically join the multicast group so that it can pull the stream.

#### TCP MPEG-TS

```
pullStream uri=dmpegtstcp://<STREAM_ADDRESS>:<PORT> localStreamName=TSTest
```

**Note:**

The “**d**” in front of mpegts ( **d**mpegts) in the URIs above refers to “deep parsing”. Using the URI, the inbound MPEG-TS stream can be re-encapsulated into other protocols such RTMP or RTSP. If the only output format will be MPEG-TS (e.g. EMS is used as an MPEG-TS pass-through), then mpegtsudp and mpegtstcp can be used as the URI protocol specifier. This will speed the transfer of the MPEG-TS streams since no parsing will occur.



### LOCAL SDP FILE

EMS is also capable in pulling an Session Description Protocol (SDP) file. An SDP is a format for describing the initialization parameters of streaming media sessions. SDP does not deliver media itself but is used for negotiation between end points of media type, format, and all associated properties.

```
pullStream uri=file://<FILEPATH>/FILENAME.sdp localStreamName=sdpFileTest
```

**Note:**

The SDP must reside in the file system accessible by EMS.