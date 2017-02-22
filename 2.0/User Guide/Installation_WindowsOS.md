![emslogo](..\emslogo.png)



# Installation Procedure For Windows

1. Download the EMS package installer at [https://evostream.com/software-downloads](https://evostream.com/software-downloads)

2. Install EMS 

   2.1. Extract the zip package

   2.2. Right-click on `setup.exe` then click **Run as administrator**

   <img src="./assets/qsgfw1.jpg" style="height:300px" />

   ​

   2.3. Select the Setup Language, click **OK**

   ![](./assets/qsgfw2.jpg)

   ​

   2.4. Click **Next** to continue the installation

   ![](./assets/qsgfw3.jpg)

   ​

   2.5 Read the license agreement and select **I accept the agreement**, click **Next**

   ![](./assets/qsgfw4.jpg)

   ​

   2.6. Verify the installation path, click **Next**

   ![](./assets/qsgfw5.jpg)

   ​

   2.7. Tick **Create a desktop icon**, click **Next**

   ![](./assets/qsgfw6.jpg)

   ​

   2.8. Confirm installation, click **Install**

   ![](./assets/qsgfw7.jpg)

   ​

   2.9. Read the information, click **Next**

   ![](./assets/qsgfw8.jpg)

   ​

   2.10. Click **Finish** to finish the installation.  

   ![](./assets/qsgfw9.jpg)

   ​

   **Note:** Uncheck **Launch EMS** if the license is not yet installed.






## License Installation

**Note:** You should already have your license file available. If none, EvoStream offers a **30-day free trial** license to those who want to explore the features of EMS. Click [here](https://evostream.com/free-trial/) to avail the free trial or contact [salesupport@evostream](mailto:salessupport@evostream.com) for other license type purchase.

To install the license, simply copy the `License.lic` file to `C:\EvoStream\config`.





## Distribution Content

```
C:\EvoStream
   ├── config
   │   ├── auth.xml
   │   ├── bandwidthlimits.xml
   │   ├── blacklist.txt
   │   ├── config.lua
   │   ├── connlimits.xml
   │   ├── ingestpoints.cml
   │   ├── pushPullSetup.xml
   │   ├── server.cert
   │   ├── server.key
   │   ├── users.lua
   │   ├── webconfig.lua
   │   └── whitelist.txt
   ├── demo
   │   ├── base64.js
   │   └── emsdemo.html
   ├── evo-avconv-presets
   │   └── [30 transcode preset files]
   ├── evo-phpengine
   ├── evo-webroot
       ├── demo
       │   ├── css
       │   ├── evo.png
       │   ├── evowrtcclient.html
       │   ├── evowsvideo.html
       │   ├── jsonMetaTest.html
       │   ├── jsonMetaWriteTest.html
       │   └── loading.gif
       ├── EMS_Web_UI
       │   ├── css
       │   ├── img
       │   ├── js
       │   ├── php
       │   ├── phpacct
       │   ├── settings
       │   ├── swf
       │   ├── evo.png
       │   ├── evostream_copyright.txt
       │   ├── index.php
       │   ├── install_license.php
       │   ├── license.txt
       │   ├── loading.gif
       │   ├── navbar.php
       │   ├── README.txt
       │   ├── README[Enable_Login_Authentication].txt
       │   └── style.css
       ├── evowebservices
       │   ├── config
       │   ├── core
       │   ├── plugins
       │   ├── evostream_copyright.txt
       │   ├── evowebservices.php   
       │   └── README.txt
       ├── clientaccesspolicy.xml
       └── crossdomain.xml
   ├── logs
   ├── media
   ├── services
   ├── emsTranscoder.bat
   ├── evo-avconv.exe
   ├── evo-mp4writer.exe
   ├── Evostream Media Server EULA v2.pdf
   ├── evostreamms.exe
   ├── evo-webserver.exe
   ├── libgcrypt-20.dll
   ├── libgmp-10.dll
   ├── libgnutls-28.dll
   ├── libgpg-error6-0.dll
   ├── libhogweed-2-5.dll
   ├── libiconv-2.dll
   ├── libmicrohttpd-12.dll
   ├── libnettle-4-7.dll
   ├── README.txt
   ├── run_console_ems.bat
   ├── tests.exe
   ├── unins000.dat
   ├── unins000.exe
   └── zlib1.dll
```