# Event Notification System

The EMS Event Notification System provides an extremely powerful way of interacting with the EMS. At the basic level it allows you to easily understand and monitor the usage of your server. You can either poll and parse the log file, or simply subscribe to the HTTP based notifications sent out by the EMS. **The notifications mean that you can have a fully RESTful monitor, gathering metrics in real time!**

Beyond monitoring and gathering metrics, you can **use the Event Notification System to create custom stream processing.** If you want to automatically create HLS/HDS/MSS/DASH streams out of new inbound streams, simply call createHLSStream/createHDSStream/createMSSStream/createDASHStream in response to each “new inbound stream” event. If you want to close inbound streams when the associated outbound stream is lost, call shutdownStream when you receive an “outbound stream closed” event.



## Configuring Event Notifications

Events can be sent to multiple destinations, or “sinks”, at the same time. A “sink” can be either a file or a network destination. Multiple sinks can be enabled at the same time, allowing you to both log events and receive them in your web service(s). These sinks can be configured so that only the events you will be consuming will be generated. Event Sinks are configured in the `config/config.lua` file.



### Enabling Event Logs

Event Notifications are off by default. To use the Event Notification System, you must modify the EMS configuration file.

1.  Remove comment to the eventLogger section in the configuration

2.  Select your preferred filename and file format

3. Configure time-stamp if to be used

4. Select events that will be enabled

   **Note:** Only the events selected will be shown in the logs



Below is the snippet of the Event Notification System logger.

```
eventLogger=
			{
				sinks=
				{
					{
						type="file",
						customData =
						{
							some="string",
							number=123.456,
							array={1, 2.345, "Hello world", true, nil}
						},
						filename="..\\logs\\events.txt",
						format="text",
						--format="xml",
						--format="json",
						--format="w3c",
						--[[
						timestamp=true,
						appendTimestamp=true,
						appendInstance=true,
						fileChunkLength=43200, -- 12 hours (in seconds)
						fileChunkTime="18:00:00",
						]]--
						enabledEvents=
						{
							"inStreamCreated",
							"outStreamCreated",
							
							--removed other list for clarity
							
						},
					},
```

**Sample Log:**

```
00001	inStreamCreated
	PID: 11376
	appName: evostreamms
	audio:
		bytesCount: 0
		codec: AAAC
		codecNumeric: 4702111241970122752
		droppedBytesCount: 0
		droppedPacketsCount: 0
		packetsCount: 0
	bandwidth: 50064
	connectionType: 1
	creationTimestamp: 1488279302365.164
	farIp: 192.168.2.21
	farPort: 554
	ip: 192.168.2.103
	name: axis
	nearIp: 192.168.2.103
	nearPort: 9372
	port: 9372
	processId: 11376
	processType: origin
	pullSettings:
		audioCodecBytes: 
		configId: 1
		emulateUserAgent: EvoStream Media Server (www.evostream.com) player
		forceTcp: false
		httpProxy: 
		isAudio: true
		keepAlive: true
		localStreamName: axis
		operationType: 1
		pageUrl: 
		ppsBytes: 
		rangeEnd: -1
		rangeStart: -2
		rtcpDetectionInterval: 10
		sendRenewStream: false
		spsBytes: 
		ssmIp: 
		swfUrl: 
		tcUrl: 
		tos: 256
		ttl: 256
		uri: rtsp://192.168.2.21/axis-media/media.amp
	queryTimestamp: 1488279302366.165
	type: INP
	typeNumeric: 5282247373882392576
	uniqueId: 1
	upTime: 1.001
	video:
		bytesCount: 0
		codec: VH264
		codecNumeric: 6217274493967007744
		droppedBytesCount: 0
		droppedPacketsCount: 0
		height: 720
		level: 41
		packetsCount: 0
		profile: 66
		width: 1280
```



### Application vs. Server Events

The config.lua file has two eventLogger sections as follows:

1. Application-owned – This is lower in the file and is “inside” the application configuration section. It configures “application level” events. **This is the recommended configuration section to modify.**
2. Server-wide (or default) – This is higher in the file and is at the outer-most variable scope level. This section configures events that are outside the application or events which the application level fails to catch. This is typically only for system events like server startup, server shutdown and application load.



## Events List

