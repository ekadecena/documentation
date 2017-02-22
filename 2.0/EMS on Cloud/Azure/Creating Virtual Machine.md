![EMS logo](C:\Users\New QA\Documents\new docs\emslogo.png)



# Creating Virtual Machine



## Getting Started

### Pre-requisites

- Microsoft Account






## Deployment

To get started with the EvoStream Media Server (EMS) on Azure, the first thing to do is to setup the virtual machine by using the **Quick Deployment** or **Setting up the Virtual Machine** from scratch. 



### A.	Quick Deployment

To lessen the time of configuring a virtual machine, clicking the links below will navigate you to the Custom Deployment Template.

- _Quick-Deploy: Steps 1 and 2 below can be skipped by clicking one of the following buttons:_  
  - _Quick-Deploy EvoStream Media Server 1.7.1 for Windows Server 2012 R2_  
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FEvoStream%2Fevostream_addons%2Fmaster%2Fazure_templates%2Fems171_windows2012%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>
  - _Quick-Deploy EvoStream Media Server 1.7.1 for Ubuntu 14.04 64-bit_  
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FEvoStream%2Fevostream_addons%2Fmaster%2Fazure_templates%2Fems171_ubuntu1404%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>


**Note:** The size of the machine used in this setup is the A5 Standard.

​	![](../assets/A5.JPG)





### B.	Setup Virtual Machine Environment

1. Search for the EvoStream Media Server in the Azure marketplace, or simply follow this [link](https://azure.microsoft.com/en-us/marketplace/partners/evostream-inc/evostream-media-server/).

   ![](../assets/homepage.JPG)

   ​

2. Select the operating system for the virtual machine to be created. Click on **Create Virtual Machine** button.

   ![](../assets/OSselect.jpg)

   ​

   **Images available:**

   - EvoStream Media Server for Windows - Windows Server 2012 R2
   - EvoStream Media Server for Ubuntu - Ubuntu 14.04 64-bit

   ​

3. **Sign in** your Microsoft Azure account if not yet signed in. You will be redirected to the EvoStream Media Server page.  Read on the notes and if ready, click on the **Create** button.

   ![](../assets/create_windows.JPG)

   ​

4. Configure the virtual machine settings based on your preferences:

   - [x] Configure basic settings

         ![](../assets/basics.JPG)


- [x] Choose virtual machine size

         **Note:** Click on View all to see all the available machine size

         ![](../assets/size.JPG)

- [x] Configure optional features

        ![](../assets/optional.JPG)

      ​

- [x] Review Summary

        ![](../assets/summary.JPG)

      ​

- [x] Buy

      ![](../assets/buy.JPG)

      ​

5. Review the **Settings**, **Offer Details** and **Terms of Use** then click **Purchase** to start the deployment

6. To check if the image has been created, on the **Microsoft Azure Dashboard**, click on the **Virtual machines**. You will now see the image created once the deployment succeeded.

**Note:** The machine is started after the deployment