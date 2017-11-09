<img class="float-right" src="https://oracle.github.io/learning-library/workshops/common-content/images/touch-the-cloud/ttc-logo.png" width="200">
# Lab 400 - HCM Integration
---

## Introduction

This is the forth of several labs that are part of the **ICS Development** workshop. 

In this lab, you will test the integration that was created in Lab 300 and see how the Integration is replicated into HCM Cloud.

## Part 1: Test the ICS Integration

---

### **1.1**: Test Using SoapUI

**3.1** Open SoapUI.  If you don't already have this installed, follow the instructions provided in the **Prerequisites** section of this workshop.

![](images/400/image052.png)

**3.2** Click on the **SOAP** button so we can create a new project for testing our new ICS SOAP Web Service

![](images/300/image089.png)

**3.3** In the **New SOAP Project** dialog window, paste the WSDL URL into the **Initial WSDL** window and give a meaningful **Project Name** such as _User03 Create EBS Order Lab 400_.  Keep the checkbox selected for **create sample requests for all operations?**.  Click on the **OK** button after you've initialized the settings for your new SoapUI SOAP project.

![](images/400/image075.png)

**3.4** The new SOAP Project will appear in the left-hand navigation.

**3.5** Expand the **createOrder** operation by clicking on it, then open the auto-generated sample request **Request 1** by double-clicking on it.  An empty request payload will be generated.

![](images/400/image076.png)

**3.6** In the request payload, as in Lab 300, replace the question marks with the following test values:

- **AccountName**: _Imaging Innovations, Inc._
- **Comment**: _Lab 400 request from SoapUI_
- **ItemID**: _2155_
- **Qty**: _1_
- **Price**: _3333_

![](images/400/image077.png)

**3.7** Next we need to add the authorization credentials so ICS will allow the request from SoapUI.  ICS uses basic username/password authentication.

**3.8** Click on the **Auth** button in the lower-left of the **Request 1** SoapUI window

**3.9** In the **Authorization** dropdown, select _Add New Authorization..._

![](images/300/image093.png)

**3.10** In the **Add Authorization** dialog pop-up window, select **Type** of _Basic_ form the picklist, then select the **OK** button.

![](images/300/image094.png)

**3.11** Fill in your assigned username and password in the **Auth (Basic)** window at the bottom of the SoapUI request window

![](images/300/image095.png)

**3.12** ICS needs two headers in the request payload to satisfy the enforced Web Services Security (WSS) standards.  It needs both the **WSS Username Token** and the **WS-Timestamp**.

**3.13** Insert the **WSS Username Token** by right-clicking in the Request payload body and select **Add WSS Username Token** from the pull-down list

![](images/300/image096.png)

**3.14** In the **Specify Password Type** dialog pop-up window, select _PasswordText_ as the WSS Username Token type, then click on the **OK** button.

![](images/300/image097.png)

**3.15** Insert the **WS-Timestamp** by right-clicking in the Request payload body and select **Add WS-Timestamp** from the pull-down list

![](images/300/image098.png)

**3.16** In the **Specify Time-To-Live value** dialog pop-up window, set the value (in milliseconds) to _60000_ (60 seconds), then click on the **OK** button.

![](images/300/image099.png)

**3.17** Finally your request payload is ready to send to ICS.

**3.18** Click on the green _Submit Request_ arrow in the upper left of the **Request 1** window.

![](images/300/image100.png)

**3.19** The right side of the **Request 1** SoapUI window will display the results of the ICS integration call.

**3.20** The return payload of the ICS integration will show the Order Number and the status of `S` for _Success_.

![](images/400/image078.png)

### **3.2:**	Verify the Order was Created in EBS

---

**3.2.1** Login to EBS using the endpoint and credentials provided to you by the workshop organizer.  You will use the user *operations*.

- *NOTE:* For the EBS instance used in this workshop, the Oracle Single Sign-On system is used to regulate access.  Unless individual users are explicitly added to have access to the EBS system, they will not be able to access the following EBS login page.  If you can't access the login page with your Oracle SSO login, then you can look at the following screenshots to see how you would be able to see your Order in an EBS R12.2 system.

![](images/400/image79.png)

**3.2.2** Select the EBS Responsibility *Order Management, HTML User Interface*:

![](images/400/image80.png)

**3.2.3** Examine the list in the *Open Orders* report and verify that your new order shows up in the list.

Note that the _Order Amount_ shown is larger than that of the quote because of shipping costs and taxes that were added automatically by EBS .

![](images/400/image81.png)

You have now completed the final lab of the ICS Developer Workshop.  

Congratulations! You should now have a much better understanding of how to work with ICS to create complex integrations.
