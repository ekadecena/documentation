![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# Connecting to EMS on Windows

After creating the EMS virtual machine,, you will need to connect to your EMS to use it. Here are the steps on how you can connect to EMS using **Remote Desktop Connection**, **EMS Web UI** and **EMS HTTP Based API**.

**Note:** All the virtual machines in your account is seen under the Virtual machines in the left-side menu bar.  Click on the Virtual Machine name. Click on **Start**.

![](../assets/startVM.JPG)





## A.	Remote Desktop Connection

1. Run the **Remote Desktop Application**

2. Enter the details of the virtual machine image, click **Connect**

   **Computer** - the IP address of the image

   **Username** - the username set for the machine

   ![](../assets/remotedesktop.jpg)

   ​

3. Enter the **password** for the user, click **OK**

   **Password**- the password set for the machine

4. The connection will be established. You may now **<u>install the license</u>** to use the EMS capabilities!

   **Note:** The EMS is installed in `C:\EvoStream`. 



## B.	EMS Web UI

While most work with the EMS happens at the command line or through the HTTP based API calls, the EMS does have a Web UI that can be used. To access the UI simply point your browser at the proper URL: `http://<DomainOrPublicIP>:8888/EMS_Web_UI/index.php`

**< DomainOrPublicIP >** will need to be replaced with the Public Domain or Public IP of your new EC2 Instance.

**Note:** EMS should be running to be able to access the EMS Web UI.



### B.1.	Determining Public IP

1. Sign in to *http://portal.azure.com/*

2. Click on virtual machine created under Virtual Machines menu

3. Start the virtual machine

4. In the Essentials pane, the Public IP address/DNS name label is displayed

   **Note:** The IP address is changing everytime the virtual machine is restarted

   ![](../assets/IPinAzure.jpg)
   ​

### B.2.Login for Web UI

The Web UI is protected by default when using the EMS on AWS.  When accessing the Web UI you will be prompted for a username and password.

![](.\assets\authentication.JPG)

- Username: evostream

- Password:  "UID" - the unique identifier of the virtual machine

  **Note:** The UID will serves as the password for the Proxy and Web UI authentication. The UID is obtained once a virtual machine is made. It can only be checked in the EMS webconfig.lua.

  ```
  apiProxy=
  {
     authentication="basic",
     pseudoDomain="apiproxy",
     address="127.0.0.1",
     port=7777,
     userName="evostream",
     password="D817E76F-B6F2-CC4F-ACAC-EAE9D84CEE3F",   --> sample UID
  }
  ```

  ​


## C.	HTTP Based API

For integration with the EMS at the software level, using the HTTP Based API is often much more useful.  The full set of API's available to you are found here: [API Definition](http://docs.evostream.com/ems_api_definition/table_of_contents)

For the EMS on AWS, the HTTP based API is exposed, but it requires authentication to be used.  We call this **Proxy Authentication**. Basic Authentication is used and so just a username and password are required:

- Username: evostream
- Password: "UID" - the unique identifier of the virtual machine, this will be seen in webconfig.lua

Command will take this general format:

```
http://Username:Password@IPAddress:Port/apiproxy/CommandName?params=<base64EncodedString>
```

**Sample Command:** 

```
http://evostream:i-D817E76F-B6F2-CC4F-ACAC-EAE9D84CEE3F@52.91.237.115:8888/apiproxy/version
```

**Note:** username is “**evostream**” and password is the “**UID**”

See EMS [documentation on HTTP](http://docs.evostream.com/ems_user_guide/runtimeapi#http) for more details.

