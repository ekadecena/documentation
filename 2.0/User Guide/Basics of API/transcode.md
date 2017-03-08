[TOC]

# transcode

The EMS is packaged with a software encoder which provides a wide variety of additional functionality to the EMS. EvoStream has chosen  LibAV’s AVConv encoder to be distributed, unmodified, along with the EMS. Source code for AVConv can be found at [http://libav.org/download.html](http://libav.org/download.html). EvoStream complies fully with the GPL in relation to the distribution of AVConv.

**The EMS can be easily configured to use ANY software encoder. If a different software encoder is desired, the integration requires only a change to a script, something that can be done on-demand.**

Transcoding is an inherently complicated process, given the huge variety of options available for compressing audio and video. The EMS provides a simple `transcode` API which makes the entire process very easy.

**Note:**

Transcoding requires **SIGNIFICANT** computing resources and will severely impact performance. A general conservative guideline is that to accomplish one transcoding job per CPU core for HD streams.



## How To

### Changing Stream Bitrates

A common use case for transcoding involves the “translating”(down-scaling) of an HD stream into lower bitrates to support Adaptive Streaming protocols and smaller clients like Android and iOS devices.

The simplest way to accomplish this is to bring the original HD stream into the EMS. You can then issue a command similar to the following to create multiple streams with lower bitrates:

**Format:**

```
transcode source=rtmp://<stream_source> groupName=<groupName> videoBitrates=<bitrate> destinations=<destinationName>
```

**Sample API Call:**

```
transcode source=rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4 groupName=group1 videoBitrates=100k,200k,300k destinations=stream100,stream200,stream300
```

**JSON Response:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- na
      -- na
      -- na
    croppings:
      -- na
      -- na
      -- na
    destinations:
      -- stream100
      -- stream200
      -- stream300
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: stream300
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName:
    source: rtmp://s2pchzxmtymn2k.cloudfront.net/cfx/st/mp4:sintel.mp4
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- stream100
      -- stream200
      -- stream300
    videoBitrates:
      -- 100k
      -- 200k
      -- 300k
    videoSizes:
      -- na
      -- na
      -- na
```

This command takes the **Source1** stream and creates 3 new streams within the EMS. **stream100** has a bit rate of 100kbps, **stream200** has a bit rate of 200kbps and **stream300** has a bit rate of 300kbps.

You can then take each of those final streams and access them directly (IE: via RTMP or RTSP), or you can create an HLS group out of them to create an adaptive bitrate stream for iOS devices:

**Creating HLS from Transcoded Stream:**

```
createhlsstream localstreamnames=stream100,stream200,stream300 targetfolder=/mywebroot/hls groupname=MyGroup playlisttype=rolling playlistLength=10 chunkLength=20
```



### Using Different Codecs

The EMS requires streams to be of type H.264/AAC, but that may not be the format your stream source is in. The EMS Transcoder can be used to convert your source stream into H.264/AAC:

**Format:**

```
transcode source=<stream_source>/localStreamName groupName=<groupName> videoBitrates=<bitrate> audioBitrates=<bitrate> destinations=<destinationName>
```

**Sample API Call:**

```
transcode source=rtsp://IpOfStreamSource:554/myStream groupName=group1 videoBitrates=5000k audioBitrates=800k destinations=myTranscodedStream
```

**JSON Response:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- 800k
    croppings:
      -- na
    destinations:
      -- myTranscodedStream
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: myTranscodedStream
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName:
    source: rtsp://127.0.0.1:5544/myStream
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- myTranscodedStream
    videoBitrates:
      -- 5000k
    videoSizes:
      -- na
```

This command pulls the source stream from its RTSP source directly, transcodes it, and passes it to the EMS as the `destinationName`. The `videoBitrates` parameter **must** be specified when transcoding the video codec. The `audioBitrates` parameter must be specified when transcoding the audio codec. If either the audio or video does not need to be transcoded, that parameter may be skipped. Here it is assumed that the source stream has a video bit rate of around 5Mbps and audio bitrate of around 800kbps.



### Use files as input and/or output:

This will change your input stream to an output file, or an input file to an output file.

```
transcode source=file://C:\videos\test.mp4 groupName=group videoBitrates=100k audioBitrates=copy destinations=file://C:\videos\out.mp4 keepAlive=0
```



### Video Overlays - Watermarking

The EMS Transcoder may be used to generate overlays on top of your videos. PNG or JPEG images with alpha layers (transparency) should be used. **The image must be at the same or smaller resolution (height and width) of the video you are overlaying**. The overlay file will be placed at the top-left corner of the video. To create the overlay, simply issue the following command:

**Format:**

```
transcode source=<localStreamName> groupName=<groupName> overlays0=<path/to/image.ext> destinations=destinationName
```

**Sample API Call:**

```
transcode source=myStream groupName=group1 overlays=/path/to/evologo.jpg destinations=OverlayedStream
```

**JSON Response:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- na
    croppings:
      -- na
    destinations:
      -- OverlayedStream
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: OverlayedStream
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName: myStream
    source: stream100
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- OverlayedStream
    videoBitrates:
      -- na
    videoSizes:
      -- na
```



### Cropping

In some cases, you may want to crop a video and focus on just a portion of the video. The EMS Transcoder supports video cropping.

**Format:**

```
transcode source=<localStreamName> groupName=<groupName> croppings=<horizontalPosition:verticalPosition:width:height> destinations=destinationName
```

**Sample API:**

```
transcode source=myStream groupName=group1 croppings=0:0:50:50 destinations=CroppedStream
```

**JSON Response:**

```
Command entered successfully!
Transcoding successfully started.

    audioBitrates:
      -- na
    croppings:
      -- 0:0:50:50
    destinations:
      -- CroppedStream
    dstUriPrefix: -f flv tcp://localhost:6666/
    emsTargetStreamName: CroppedStream
    fullBinaryPath: C:\EvoStream_171\emsTranscoder.bat
    groupName: group1
    keepAlive: true
    localStreamName: myStream
    source: myStream
    srcUriPrefix: rtsp://localhost:5544/
    targetStreamNames:
      -- CroppedStream
    videoBitrates:
      -- na
    videoSizes:
      -- na

```

This creates a resultant stream containing only a square 50px by 50px from the top right corner of the video. The format for the `croppings` parameter horizontalPosition:verticalPosition:width:height where horizontalPosition=0 at leftmost pixel, verticalPosition=0 at uppermost pixel.



### Force TCP for inbound RTSP

```
transcode source=rtmp://<RTMP server>/live/streamname groupName=group videoBitrates=copy videoSizes=360x200 $EMS_RTSP_TRANSPORT=tcp
```



## Stopping Transcoding Process(es)

You need to Issue a `removeconfig` API to stop the transcoding. 

**Format:**

```
removeConfig groupName=<groupName>
```

**Sample API Call:**

```
removeConfig groupName=group1
```

**JSON Response:**

```
Command entered successfully!
Configuration terminated
```

All transcoding processes under **group1** will be removed.



