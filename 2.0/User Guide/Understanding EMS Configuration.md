![emslogo](..\emslogo.png)





# EMS Configuration



## A. auth.xml

The configuration for the authentication. If true, the authentication declared in users.lua will be read before the streaming starts.

```
<?xml version="1.0" ?>
<BOOL name="">true</BOOL>
```

See [users.lua](#K. users.lua).



## B. bandwidthlimits.xml

Defines the maximum amount of bandwidth you want the server to be able to use (set the instantaneous bandwidth cap).

If `enableCheckBandwidth` in config.lua is true, automatically EMS will read the bandwidths.xml file. EMS will limit all the incoming and outgoing stream dependent to the configured bandwidth range.

Default for in and out is zero (0) which means no limit.

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <DOUBLE name="in">0.000</DOUBLE>
    <DOUBLE name="out">0.000</DOUBLE>
</MAP>
```

See [enableCheckBandwidth](# enableCheckBandwidth).



## C. blacklist.txt

Defines the IP address that will be blocked by EMS. If a blacklist is specified, access will only be granted to IP address does **NOT APPEAR** on the blacklist.

**Implementation:** 

| Blacklist | Whitelist | Is Allowed?                            |
| :-------: | :-------: | -------------------------------------- |
|   empty   |   empty   | all IPs are allowed                    |
|  x.x.x.x  |   empty   | all IPs are allowed except for x.x.x.x |
|   empty   |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  y.y.y.y  | only y.y.y.y is allowed                |
|  no file  |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  no file  | all IPs are allowed except for x.x.x.x |
|  no file  |  no file  | error                                  |

**Notes:**

- `enableIPFilter` should be set to `true` in webconfig.lua to be able to read the blacklist file

- `blacklistFile` code should not be commented to be able to honor the list of blacklisted IP address

  ```
    enableIPFilter=true,
    whitelistFile="..\\config\\whitelist.txt",
    blacklistFile="..\\config\\blacklist.txt",
  ```

- If IP address is both on whitelist and blacklist file, EMS will treat the IP address as blacklisted


See [whitelist.txt](#M. whitelist.txt).



## D. config.lua

This is the main configuration file for the EMS. This file defines all of the startup parameters used by the server, including the location and names of all of the other configuration files. If you wish to change the name of any of the subsequent configuration files, you can do so here. This file is also just a command-line parameter to the EMS executable. The run-scripts provided with the EMS distribution use this file by default. If you want to change the location or name of this file you can simply modify the run scripts to use a different file.

The EMS configuration file, config.lua, is a hierarchical data structure of assignments (key names with values). It is sent as a parameter when running the EvoStream server. The format is as follows:

-  **`<keyname>= <value>`**

  where `value` could be any of the following types:
  - string = series of alpha numeric characters (should be enclosed in double quotes)

    ```
    Example:	pushPullPersistenceFile="..\\config\\pushPullSetup.xml",
    ```

  - number = digits

    ```
    Example:	streamsExpireTimer=10,
    ```

  - array = list of values (separated by comma and is grouped by braces {}, each value enclosed in double quotes)

    ```
    Example:	aliases = {“flvplayback1”, “vod1”, “live”}
    ```


-  **`<keyname>= <object>`**

  where `object`is a list of assignments enclosed by braces {}

  ```
  configurations =
  {
      daemon = "true",
      pathSeparator = "/",
      logAppenders = {...},
      applications = {...}
  }
  ```

**Note:** 

If you modify this file and the server then fails to start, you have made an error. You can either roll-back your changes or you can use the `--use-implicit-console-appender` command line parameter to get extra debug information about what failed during startup.



### The config.lua:

#### A. pathSeparator

This is the path separator used by EMS.

```
pathSeparator="/",
```

#### B. logAppenders

This is the configuration for the EMS logs.

```
logAppenders=
	{
		{
			name="console appender",
			type="coloredConsole",
			level=6
		},
		{
			name="file appender",
			type="file",
			level=6,
			fileName="..\\logs\\evostream",
			newLineCharacters="\n",
			fileHistorySize=100,
			fileLength=1024*1024,
			singleLine=true
		},
	},
```

#### C. applications

- **rootDirectory** - the root directory of the EMS

  ```
  rootDirectory="./",
  ```


- **appDir** - the application directory of EMS

  ```
  appDir="./",
  ```


- **name** - the name of the server

  ```
  name="evostreamms",
  ```


- **description** - the description of the server

  ```
  description="EVOSTREAM MEDIA SERVER",
  ```


- **protocol** - 

  ```
  protocol="dynamiclinklibrary",
  ```


- **default**

  ```
  default=true,
  ```


- **pushPullPersistenceFile** - the path of the pushPull configuration file

  ```
  pushPullPersistenceFile="..\\config\\pushPullSetup.xml",
  ```


- **authPersistenceFile** - the path of the authentication file

  ```
  authPersistenceFile="..\\config\\auth.xml",
  ```


- **connectionsLimitPersistenceFile** - the path of the connection limit file

  ```
  connectionsLimitPersistenceFile="..\\config\\connlimits.xml",
  ```


- **bandwidthLimitPersistenceFile** - the path of the bandwidth limit file

  ```
  bandwidthLimitPersistenceFile="..\\config\\bandwidthlimits.xml",
  ```


- **ingestPointsPersistenceFile** - the path of the ingest points file

  ```
  ingestPointsPersistenceFile="..\\config\\ingestpoints.xml",
  ```


- **streamsExpireTimer** - 

  ```
  streamsExpireTimer=10,
  ```


- **rtcpDetectionInterval**

  ```
  rtcpDetectionInterval=15,
  ```


- **hasStreamAliases** - enables or disables stream name aliases

  ```
  hasStreamAliases=false,
  ```


- **hasIngestPoints** - the configuration of the ingest point 

  ```
  hasIngestPoints=false
  ```


- **validateHandshake** - 

  ```
  validateHandshake=false,
  ```


- **aliases** - the extension of the stream where alias can be added

  ```
  aliases={"er", "live", "vod"},
  ```


- **maxRtmpOutBuffer** - 

  ```
  maxRtmpOutBuffer=512*1024,
  ```


- **hlsVersion** - the HLS version to be used 

  ```
  hlsVersion=3,
  ```

  Supported versions:

  - HLS version 3
  - HLS version 4
  - HLS version 5
  - HLS version 6

  For more information about HLS click [here](https://developer.apple.com/library/content/referencelibrary/GettingStarted/AboutHTTPLiveStreaming/about/about.html).


- **useSourcePts** - 

  ```
  useSourcePts=false,
  ```


- **enableCheckBandwidth** - reads the bandwidth.xml if set to true

  ```
  enableCheckBandwidth=true,
  ```


- **vodRedirectRtmpIp** - the IP of the other server where EMS can get the source VOD file.

  **How it works?** The local server will look for video1. When that lookup fails it will get the configuration details set to `vodRedirectRtmpIp` parameter. If there's a valid value, the local server makes a `pullStream` request on the server (vodRedirectRtmpIP value) for video1. The local server then uses that new stream resulting from the `pullStream` to serve the initial client request.

  ```
  vodRedirectRtmpIp="",
  ```

  **Note:** This will only access the mediaFolder. Make sure that the VOD files are inside the mediaFolder or else, searching for the source is on loop.


- **forceRtmpDatarate**

  ```
  forceRtmpDatarate=false,
  ```


- **mediaStorage** - the configuration for the media storage

  ```
  mediaStorage = {
  				recordedStreamsStorage="../media",
  				{
  					description="Default media storage",
  					mediaFolder="../media",
  				},
  				--[[
  				-- the following is an example and contains all
  				-- available properties along with their default
  				-- values(except paths, of course)
  				sample={
  					description="Storage example",
  					mediaFolder="/some/media/folder",
  					metaFolder="/fast/discardable/separate/folder",
  					enableStats=false,
  					clientSideBuffer=15,
  					keyframeSeek=true,
  					seekGranularity=0.1,
  					externalSeekGenerator=false,
  				}
  				]]--
  			},
  ```


- **acceptors** - the default acceptors used by EMS

  ```
  acceptors=
  			{
  				-- CLI acceptors
  				{
  					ip="0.0.0.0",
  					port=1112,
  					protocol="inboundJsonCli",
  					useLengthPadding=true
  				},
  				{
  					ip="0.0.0.0",
  					port=7777,
  					protocol="inboundHttpJsonCli"
  				},
  				{
  					ip="0.0.0.0",
  					port=1222,
  					protocol="inboundAsciiCli",
  					useLengthPadding=true
  				},

  				-- RTMP and clustering
  				{
  					ip="0.0.0.0",
  					port=1935,
  					protocol="inboundRtmp",
  				},
  				{
  					ip="127.0.0.1",
  					port=1936,
  					protocol="inboundRtmp",
  					clustering=true
  				},
  				{
  					ip="127.0.0.1",
  					port=1113,
  					protocol="inboundBinVariant",
  					clustering=true
  				},

  				-- RTSP
  				{
  					ip="0.0.0.0",
  					port=5544,
  					protocol="inboundRtsp",
  					--[[
  					multicast=
  					{
  						ip="224.2.1.39",
  						ttl=127,
  					}
  					]]--
  				},

  				-- LiveFLV ingest
  				{
  					ip="0.0.0.0",
  					port=6666,
  					protocol="inboundLiveFlv",
  					waitForMetadata=true,
  				},

  				--[[
  				-- Inbound TCP TS
  				{
  					ip="0.0.0.0",
  					port=9999,
  					protocol="inboundTcpTs",
  				},

  				-- Inbound UDP TS
  				{
  					ip="0.0.0.0",
  					port=9999,
  					protocol="inboundUdpTs",
  				},
  				]]--

  				-- HTTP
  				{
  					ip="0.0.0.0",
  					port=8080,
  					protocol="inboundHttp",
  				},

  				--RTMPS
  				--[[
  				{
  					ip="0.0.0.0",
  					port=4443,
  					protocol="inboundRtmp",
  					-- cipherSuite="!DEFAULT:RC4-SHA", -- enables/disables a specific set of ciphers. If not specified, it is defaulted to the openssl collection of ciphers
  					sslKey="/path/to/some/key",
  					sslCert="/path/to/some/cert",
  				},
  				]]--
  				-- JSONMETA
  				{
  					ip="0.0.0.0",
  					port=8100,
  					--streamname="test",
  					protocol="inboundJsonMeta",
  				},
  				-- WebSockets JSON Metadata
  				{
  					ip="0.0.0.0",
  					port=8210,
  					protocol="wsJsonMeta",
  					-- streamname="~0~0~0~"
  				},
  				-- WebSockets FMP4 Fetch
  				{
  					ip="0.0.0.0",
  					port=8410,
  					protocol="inboundWSFMP4"
  				},
  			},
  ```


- autoDASH/HLS/HDS/MSS - if enabled, will automatically create the HTTP streams from the pulled entries. 

  ```
  autoDASH=
  			{
  				targetFolder= "..\\evo-webroot",
  			},
  autoHLS=
  			{
  				targetFolder= "..\\evo-webroot",
  			},
  autoHDS=
  			{
  				targetFolder= "..\\evo-webroot",
  			},
  autoMSS=
  			{
  				targetFolder= "..\\evo-webroot",
  			},
  ```

  **Note:** You can add other parameters associated with the API. See [API documetation](insert link here) for parameter lists.


- **authentication** - the authentication settings for RTMP and RTSP protocols. For RTMP, another file, `auth.xml`, is required to enable authentication. In addition, a users file, typically named `users.lua`, provides the user names and passwords.

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
  					--authenticatePlay=false,
  				}
  			},
  ```

  **authentication Structure Table:**

  | Protocol |    Parameter     | Mandatory |        Typical Setting        |
  | :------: | :--------------: | :-------: | :---------------------------: |
  |   RTMP   |       type       |   true    |            “adobe”            |
  |   RTMP   |  encoderAgents   |   true    |     “FMLE…” *(see below)*     |
  |   RTMP   |    usersFile     |   true    |     ”../config/users.lua”     |
  |   RTSP   |    usersFile     |   true    |     ”../config/users.lua”     |
  |   RTSP   | authenticatePlay |   false   | true (default value is false) |

  **Notes:**

  1. Authentication is disabled if the “authentication” block in the “config.lua” file is missing or incomplete. For RTMP protocol, authentication is disabled if the “auth.xml” file is missing or contains a “false” setting. For RTSP protocol, authentication is disabled if “authenticatePlay” in the “rtsp” block is omitted or set to “false”.
  2. Scripts are available for creating certificates and keys for EMS. Please refer to our GitHub files [here](https://github.com/EvoStream/evostream_addons/tree/master/certificates_and_keys) for details.

- **eventLogger** - the configuration for the events and event log

  ```
  eventLogger=
  			{
  				sinks=
  				{
  					--[=[
  					{
  						type="file",
  						--[[
  						customData =
  						{
  							some="string",
  							number=123.456,
  							array={1, 2.345, "Hello world", true, nil}
  						},
  						]]--
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
  							--removed other list of event for clarity--	
  						},
  					},
  					]=]--
  					{
  						type="RPC",
  						url="http://127.0.0.1:8888/evowebservices/evowebservices.php",
  						serializerType="JSON",
  						enabledEvents=
  						{  --These are the events sent by default and tend to be the most commonly used
  							"inStreamCreated",
                                   "outStreamCreated",
                                   "inStreamClosed",
                                   "outStreamClosed",
  							"streamingSessionStarted",
                                   "streamingSessionEnded",
                                   "recordChunkClosed",
  							"hlsChunkClosed",
  							--removed other list of event for clarity--						
  						},
  					},
  				},
  			},
  ```

  **Notes:** 

  1. This section is disabled by default. See events definitions [here]()
  2. The event log files will be stored in the path where EMS logs are configured


- **transcoder** - the configuration for the transcoder

  ```
  transcoder = {
  				scriptPath="..\\emsTranscoder.bat",
  				srcUriPrefix="rtsp://localhost:5544/",
  				dstUriPrefix="-f flv tcp://localhost:6666/"
  			},
  ```


- **mp4BinPath** - the path to the mp4 writer executable file

  ```
  mp4BinPath="..\\evo-mp4writer.exe",
  ```


- **webRTC** - the security configuration for the webRTC

  ```
  webrtc = {
  			sslKey="..\\config\\server.key",
  			sslCert="..\\config\\server.cert",
  		},
  ```


- **drm** - the configuration for the HLS security 

  ```
  drm={
  			type="verimatrix",
  			requestTimer=1,
  			reserveKeys=10,
  			reserveIds=10,
  			-- urlPrefix="http://server1.evostream1.com:12684/CAB/keyfile"
  			urlPrefix="http://vcas3multicas1.verimatrix.com:12684/CAB/keyfile"
  	},
  ```



## E. connlimits.xml

This file sets the allowed maximum number of connections to EMS.

Default is zero (0) means no maximum.

```
<?xml version="1.0" ?>
<UINT32 name="">0</UINT32>

```



## F. ingestpoints.xml

The file where the ingest points are saved. This should be set to true when ingest point will be used.

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
</MAP>
```



## G. License.lic

This file is needed to start everything! This file will give you access to the EMS API's. It should be placed in the right path or else EMS will not work.  To obtain a license file, click [here](https://evostream.com/free-trial/) to avail the free trial or contact [salesupport@evostream](mailto:salessupport@evostream.com) for other license type purchase.



## H. pushPullSetup.xml

This file is used by the EMS to store stream action commands that are made through the Runtime API. The most important thing to know about the pushPullSetup.xml file is that it **should not be modified manually**!. At startup, if the EMS detects that the file has been modified it will rename the file and start with a blank/fresh copy.

This file is used for internal purposes only. If, during startup, the EMS detects that changes have been made to the pushPullSetup.xml file, it will rename the existing pushPullSetup.xml file and start with a fresh configuration.

Now that the disclaimer is out of the way, it is important to understand how this file is used. When a `pullStream`, `pushStream`, `createHLSStream`, `createHDSStream`, `createMSSStream`, `createDASHStream`, `record`, or `launchProcess`, or `startWebRtc` command is executed, that command is logged to this file (assuming the `keepAlive` flag is **1**, which it is by default). 

When the EMS is started, it parses this file and attempts to recreate all of the connections. These configuration entries can be removed by issuing `removeConfig` commands, or by setting the `keepAlive` flag to **0** when the initial command is made.

**Note:** If you wish to have a “clean start” of the server, with no previous streams, you may delete this file before starting the EMS.

```
<?xml version="1.0" ?>
<MAP isArray="false" name="">
    <STR name="checksum">b494b8cb7cc5d31ebd4af75b08819139</STR>
    <MAP isArray="true" name="dash" />
    <MAP isArray="true" name="hds" />
    <MAP isArray="true" name="hls" />
    <MAP isArray="true" name="mss" />
    <MAP isArray="true" name="process" />
    <MAP isArray="true" name="pull">
    <MAP isArray="true" name="push" />
    <MAP isArray="true" name="record" />
    <MAP isArray="false" name="serverVersion">
        <STR name="banner">EvoStream Media Server (www.evostream.com) version 1.7.1 build 4491 with hash: 64b305253110afc4acd5aeaf87f0a0b0f9b53526 on branch: origin/release/1.7.0.1 - PacMan|m| - (built for Windows-8.1-x86_64 on 2016-06-17T09:33:23.000)</STR>
        <STR name="branchName">origin/release/1.7.0.1</STR>
        <STR name="buildDate">2016-06-17T09:33:23.000</STR>
        <STR name="buildNumber">4491</STR>
        <STR name="codeName">PacMan|m|</STR>
        <STR name="hash">64b305253110afc4acd5aeaf87f0a0b0f9b53526</STR>
        <STR name="releaseNumber">1.7.1</STR>
    </MAP>
    <UINT32 name="version">26</UINT32>
    <MAP isArray="true" name="webrtc" />
</MAP>

```



## I. server.cert

The certificate used for security authentication.

```
-----BEGIN CERTIFICATE-----
MIIDDDCCAnWgAwIBAgIJAOh9kCLgEMuhMA0GCSqGSIb3DQEBBQUAMIGeMQswCQYD
VQQGEwJVUzETMBEGA1UECAwKQ2FsaWZvcm5pYTESMBAGA1UEBwwJU2FuIERpZWdv
MRIwEAYDVQQKDAlldm9zdHJlYW0xEjAQBgNVBAsMCWV2b3N0cmVhbTEWMBQGA1UE
AwwNZXZvc3RyZWFtLmNvbTEmMCQGCSqGSIb3DQEJARYXYm1laXNzbmVyQGV2b3N0
cmVhbS5jb20wHhcNMTQxMTExMDc0NDI3WhcNNDkxMjMxMDc0NDI3WjCBnjELMAkG
A1UEBhMCVVMxEzARBgNVBAgMCkNhbGlmb3JuaWExEjAQBgNVBAcMCVNhbiBEaWVn
bzESMBAGA1UECgwJZXZvc3RyZWFtMRIwEAYDVQQLDAlldm9zdHJlYW0xFjAUBgNV
BAMMDWV2b3N0cmVhbS5jb20xJjAkBgkqhkiG9w0BCQEWF2JtZWlzc25lckBldm9z
dHJlYW0uY29tMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCwVGvra2hX2utJ
nriY89Wq0bsUrotH6wFlIoXbP7u5EEwKiqetvZxkUbeVxJtfdoS0OIHf+xiugYBY
33G3odSL7ZISkHT5VeDbXtBJ2kaYcMXUTlh30OPvK8MGsPPBKu5HLTPYnQiRhJc+
OcF0/oSR1oR1YGJIgfGQxXTdQFf9eQIDAQABo1AwTjAdBgNVHQ4EFgQUyjNOifTW
ufpZfEsw/2NZ7gZ8rBIwHwYDVR0jBBgwFoAUyjNOifTWufpZfEsw/2NZ7gZ8rBIw
DAYDVR0TBAUwAwEB/zANBgkqhkiG9w0BAQUFAAOBgQA+vYyx78cg2CvKTT2L2KQj
LeexZtCIHElVA+TTPmy3lY1noKXY3x0DVEjgkVE0CY9Eb5/TGoLIe2Nm/vgF2RXL
KCpVM/N34MI3wiLXbbRQUmFELtLhzhp6NFZz1PIQgl67bYiYUJ1MHcbEeZMLVely
sjiyBNWZUq1pE3x0RnTpUA==
-----END CERTIFICATE-----
```

**Note:** Scripts are available for creating certificates and keys for EMS. Please refer to our GitHub files [here](https://github.com/EvoStream/evostream_addons/tree/master/certificates_and_keys) for details.



## J. server.key

The private key used for security authentication.

```
-----BEGIN RSA PRIVATE KEY-----
MIICXAIBAAKBgQCwVGvra2hX2utJnriY89Wq0bsUrotH6wFlIoXbP7u5EEwKiqet
vZxkUbeVxJtfdoS0OIHf+xiugYBY33G3odSL7ZISkHT5VeDbXtBJ2kaYcMXUTlh3
0OPvK8MGsPPBKu5HLTPYnQiRhJc+OcF0/oSR1oR1YGJIgfGQxXTdQFf9eQIDAQAB
AoGARpKjVuf4LSGLhj2meGEvJV0n2VE6oaAnQMkede/+PEWPibCRB/KZw3UJW0ID
RaPz3QW4xWKEMGPYcLmNlAeLP4O6OK01FZidjznqFFOwLP4nau3WOoyTqIBQN1/3
il0QrPnXSvk8ao2xk4SAI87khGyiP+R1zVpBpx2nUHdDbGECQQDcLbYnJozkeFVj
0atV0vEOTQrIKv/s0ldHHJBvm8slDvWhOie8Ls41U/Jr/Rp1V/u6CdQMTSl5NB6R
SgE4NsBFAkEAzQRwA79+NXPEqcK7CbAZeURJ0H9Ad3+db+B1MwvZyqi9wjLCJeXF
AbrIkpE6jXcedtQuXtI/sJ5bglvfRDFdpQJBAL1TyUgNDCYBm1uEFZJtGr8zXEwX
PY5EqKwLUd/G1X3+SRTkTvqwPLz6fICDWdcBWwH0JZSWXU1NleNVAYt2+QkCQCCD
5agShNfBZp1t7vAYZ9HdzL8uj3DkYnnN5YiVBpOns4DLQBN2n4oor4rfUaQCEmjS
OhB70/IVC3pfS8eq9KkCQDr4ATT8i8IQyJGerJ47mx2/LhL1ZwqykqBQFW8Xyni7
GVOnuh7pX19wgj2VZv2Mz4HvKggPvXlS/WKtPFYsqsw=
-----END RSA PRIVATE KEY-----
```

**Note:** Scripts are available for creating certificates and keys for EMS. Please refer to our GitHub files [here](https://github.com/EvoStream/evostream_addons/tree/master/certificates_and_keys) for details.



## K. users.lua

Defines the valid authentication the server will require when streams are pushed into the EMS.

Where:

- user1 = name of first user

- user2 - name of second user

- password1 = password of the first user

- password2 = password of the second user


```
users=
{
	user1="password1",
	user2="password2",
}

realms=
{
	{
		name="EVOSTREAM stream router",
		method="Digest",
		users={
			"user1",
			"user2",
		},
	},
}
```

**Note:** You may add or delete number of users in this file.



## L. webconfig.lua

This is the main configuration file of the EvoStream Web Server (EWS). This file sets the locations of important web server files/folders such as the web root folder, server key & certificate, white list, black list, logs, etc. This is where other web server settings are defined, including HTTP port, group name aliasing, SSL mode, connection/memory limits, mime types, etc.

- **logAppenders** - the configuration for the web server logs and log files

  ```
  logAppenders=
  	{
  		{
  			name="console appender",
  			type="coloredConsole",
  			level=6
  		},
  		{
  			name="file appender",
  			type="delayedFile",
  			level=6,
  			fileName="..\\logs\\evo-webserver",
  			newLineCharacters="\n",
  			fileHistorySize=100,
  			fileLength=1024*1024,
  			singleLine=true
  		},
  	},
  ```

- **rootDirectory** - the root directory of the EMS

  ```
  rootDirectory="./",
  ```

- name - the name of the web server

  ```
  name="webserver",
  ```

- description

  ```
  description="Built-In Web Server",
  ```


- port

  ```
  port=8888,
  ```

- emsPort

  ```
  emsPort=1113,
  ```

  **Note:** should match config.lua's **inboundBinVariant** acceptor

- bindToIP

  ```
  bindToIP="",
  ```

- sslMode

  ```
  sslMode="disabled", 
  ```

  Accepted values:

  ​	disabled - 

  ​	enabled - 

  ​	automatic - 

- useIPV6

  ```
  useIPV6=false,
  ```

- enableIPFilter - if true, will read the blacklist and whitelist files

  ```
  enableIPFilter=false,
  ```

- whitelistFile - the path of the whitelist file

  ```
  whitelistFile="..\\config\\whitelist.txt",
  ```

- blacklistFile - the path of the blacklist file

  ```
  blacklistFile="..\\config\\blacklist.txt",
  ```

- sslKeyFile - the path of the SSL key file

  ```
  sslKeyFile="..\\config\\server.key",
  ```

- sslCertFile - the path of the SSL certificate file

  ```
  sslCertFile="..\\config\\server.cert",
  ```

- hasGroupNameAliases - enables or disables group name aliases

  ```
  hasGroupNameAliases=false,
  ```

- webRootFolder - the location of the webroot folder

  ```
  webRootFolder="..\\evo-webroot",
  ```

  **Note:** take note of the ports being used when using other webroot

- enableRangeRequests - will enable trigger to use the seek bar in forwarding or rewinding streams

  ```
  enableRangeRequests=true,
  ```

- mediaFileDownloadTimeout

  ```
  mediaFileDownloadTimeout=30,
  ```

- supportedMimeTypes

  ```
  	supportedMimeTypes=
  			{
  				-- non-streaming
  				{	
  					extensions="mp4,mp4v,mpg4",
  					mimeType="video/mp4",
  					streamType="",
  					isManifest=false,
  				},
  				{
  					extensions="flv",
  					mimeType="video/x-flv",
  					streamType="",
  					isManifest=false,
  				},
  				-- streaming
  				{
  					extensions="m3u,m3u8",
  					mimeType="audio/x-mpegurl",
  					streamType="hls",
  					isManifest=true,
  				},
  				{
  					extensions="ts",
  					mimeType="video/mp2t",
  					streamType="hls",
  					isManifest=false,
  				},
  				{
  					extensions="aac",
  					mimeType="audio/aac",
  					streamType="hls",
  					isManifest=false,
  				},
  				{
  					extensions="f4m",
  					mimeType="application/f4m+xml",
  					streamType="hds",
  					isManifest=true,
  				},
  				{
  					extensions="ismc,isma,ismv",
  					mimeType="application/octet-stream",
  					streamType="mss",
  					isManifest=true,
  				},
  				{
  					extensions="fmp4",
  					mimeType="video/mp4",
  					streamType="mss",
  					isManifest=false,
  				},
  				{
  					extensions="mpd",
  					mimeType="application/dash+xml",
  					streamType="dash",
  					isManifest=true,
  				},
  				{
  					extensions="m4s",
  					mimeType="video/mp4",
  					streamType="dash",
  					isManifest=false,
  				},
  				{ -- needed for supporting adobe player's crossdomain.xml
  					extensions="xml",
  					mimeType="application/xml",
  					streamType="",
  					isManifest=false,
  				},
  			},
  ```

- includeResponseHeaders

  ```
  includeResponseHeaders=
  			{
  				{
  					header="Access-Control-Allow-Origin",
  					content="*",
  					override=true,
  				},
  				{
  					header="User-Agent",
  					content="Evostream",
  					override=false,
  				},
  			},
  ```

- apiProxy

  ```
  apiProxy=
  			{
  				authentication="basic", -- none, basic			
  				pseudoDomain="<domain>",
  				address="127.0.0.1",
  				port=7777,
  				userName="<username>",
  				password="<password>",
  			},
  ```

- auth

  ```
  auth=
  			{
  				{
  					domain="EMS_Web_UI", --the domain folder
       				 digestFile="../evo-webroot/EMS_Web_UI/settings/passwords/.htdigest", --relative path to digest file
       				 enable=false,
  				},
  			},
  ```





## M. whitelist.txt

Defines the IP address that will have access to EMS. If a whitelist is specified, access will only be granted to that IP address that **APPEARS** on the whitelist file.

**Implementation:** 

| Blacklist | Whitelist | Is Allowed?                            |
| :-------: | :-------: | -------------------------------------- |
|   empty   |   empty   | all IPs are allowed                    |
|  x.x.x.x  |   empty   | all IPs are allowed except for x.x.x.x |
|   empty   |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  y.y.y.y  | only y.y.y.y is allowed                |
|  no file  |  y.y.y.y  | only y.y.y.y is allowed                |
|  x.x.x.x  |  no file  | all IPs are allowed except for x.x.x.x |
|  no file  |  no file  | error                                  |

**Notes:**

- `enableIPFilter` should be set to `true` in webconfig.lua to be able to read the whitelist file

- `whitelistFile` code should not be commented to be able to honor the list of whitelist IP address

  ```
    enableIPFilter=true,
    whitelistFile="..\\config\\whitelist.txt",
    blacklistFile="..\\config\\blacklist.txt",
  ```

- If IP address is both on whitelist and blacklist file, EMS will treat the IP address as blacklisted