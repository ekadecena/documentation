# HTML 5 WebRTC



## Playing Videos Using webRTC

1. To play streams from EMS using webRTC, the following command needs to be executed first on EMS. See `startWebRTC` API [here]():

   ```
    startwebrtc ersip=52.6.14.61 ersport=3535 roomid=MyRoom

   ```

   **Note:**

   The room name should be unique as much as possible, especially when using the public ERS to prevent  room name conflicts. If the room name is already taken, EMS would return an error on the console logs to indicate such scenario.

2. Access the test page `demo/evowrtcclient.html` and use the matching room ID and existing stream name on EMS as parameter to the request:

   ```
   http://<WEBSERVER_IP_ADDRESS>/demo/evowrtcclient.html?room=MyRoom&stream=MyStream

   ```

   The video will play automatically once it has successfully connected with EMS.

   ![](./assets/webrtc.jpg)

