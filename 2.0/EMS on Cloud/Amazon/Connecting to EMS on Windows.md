![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# Connecting to EMS on Windows

After creating the EMS instance, you will need to connect to your EMS to use it. Here are the steps on how you can connect to EMS using **Remote Desktop Connection**, **EMS Web UI** and **EMS HTTP Based API**.



## A.	Remote Desktop Connection

1. Run the **Remote Desktop Application**

2. Enter the details of the virtual machine image, click **Connect**

   **Computer** - the IP address of the image

   **Username** -Administrator

   **Password**- *see below*

   ​

   2.1.	How to obtain the password?

   To get the password, right click on the instance under the Instances list. Click **Connect** and you will be prompted with this:

   ![](..\assets\password.jpg)

   ​

   2.2. Click on **Get Password**. Choose the **[key-pair-name\].pem** then click **Decrypt Password**. 

   A **password** will be shown on the window.

   ![](..\assets\decrypt.JPG)

   ​

3. Enter the **password** for the user, click **OK**

4. The connection will be established. Run EMS by double clicking the desktop shortcut icon or running the `run_console_ems.bat`. You can now use the EMS capabilities!

**Note:** The EMS is installed in `C:\EvoStream`. 



## B.	EMS Web UI

While most work with the EMS happens at the command line or through the HTTP based API calls, the EMS does have a Web UI that can be used. To access the UI simply point your browser at the proper URL: `http://<DomainOrPublicIP>:8888/EMS_Web_UI/index.php`

**< DomainOrPublicIP >** will need to be replaced with the Public Domain or Public IP of your new EC2 Instance.

**Note:** EMS should be running to be able to access the EMS Web UI.



### B.1.	Determining Public IP

1. Sign in to *https://console.aws.amazon.com*

2. Click on the **EC2** under compute

   ![](..\assets\image23.jpeg)

3. In the Navigation pane of the EC2 Management Console, under Instances, click **Instances**.

4. Select the running instance.

5. In the lower pane, click the **Description tab**. The Public DNS value is the public domain name of your running instance and the Instance ID is the instances instance ID.

   ![](..\assets\image13.jpeg)

   ​

### B.2.Login for Web UI

The Web UI is protected by default when using the EMS on AWS.  When accessing the Web UI you will be prompted for a username and password.

![](..\assets\authentication.JPG)

- Username: evostream

- Password: "Amazon Instance ID" - this will need to be obtained via your Amazon account.

  **Getting the Amazon Instance ID**

  **From Amazon Console**

  1. Sign in to *https://console.aws.amazon.com*

  2. Click on the **EC2** under compute

     ![](..\assets\image23.jpeg)

  3. Click on **Running Instances** under Resources

     ![](..\assets\image24.jpeg)

     ​

  4. Click on the **Instance Name** provided for the EMS, and look for the **Instance ID** given.  This will be your password.

     ![](..\assets\image25.jpeg)




## C.	HTTP Based API

The above instructions gave you access to the EMS via the command line.  For integration with the EMS at the software level, using the HTTP Based API is often much more useful.  The full set of API's available to you are found here: [API Definition](http://docs.evostream.com/ems_api_definition/table_of_contents)

For the EMS on AWS, the HTTP based API is exposed, but it requires authentication to be used.  We call this **Proxy Authentication**. Basic Authentication is used and so just a username and password are required:

- Username: evostream
- Password: "Amazon Instance ID" - this will need to be obtained via your Amazon account as explained above.

**Command will take this general format:**

```
http://Username:Password@IPAddress:Port/apiproxy/CommandName?params=<base64EncodedString>
```

Run the command in a browser.  Copy the command in a browser URL then press **Enter**.

**Sample Command:** 

```
http://evostream:i-013c03dc9bab9d69f@52.91.237.115:8888/apiproxy/version
```

**Note:** username is “**evostream**” and password is the “**instance ID**”

See EMS [documentation on HTTP](http://docs.evostream.com/ems_user_guide/runtimeapi#http) for more details.

