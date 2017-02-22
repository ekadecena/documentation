![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# stopWebRTC



## Definition

Stops the WebRTC Signalling client to an ERS (Evostream Rendezvous Server)





## API Parameter Table

This function has no parameters.



## API Call Template

``` 
stopwebrtc
```



### Success Response in JSON

``` 
{
"data":{
    "ersip":"52.6.14.61",
    "ersport":3535,
    "roomid":"testRoom"
},
"description":"Stopped WebRTC Negotiation Service",
"status":"SUCCESS"
}
```



#### JSON Response

The JSON response contains the following details:

- data– Nothing to parse for this command
  - ersip – The IP address of the ERS
  - ersport – The port of the ERS
  - roomId – The room identifier
- description– Describes the result of parsing/executing the command
- status – **SUCCESS** if the command was parsed and executed successfully, **FAIL** if not.

------

## Notes

- ​
- ​





## **Related Links**

- Link 1
- Link 2