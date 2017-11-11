# Lab 300 - Create Integration Flow

---
## Check your Connections

### Part 1: Create the ICS Connections

 **1.1**: Login to the ICS Service Console

 ---

 **1.1.1** If you are not already logged in: From your browser (Firefox or Chrome recommended) login to the ICS Console using the following URL:
 <https://ttcics-gse00011451.integration.us2.oraclecloud.com/ics/faces/global>

 **1.1.2** Enter your `User Name` and `Password` and click **Sign In**

 ***NOTE:*** the **User Name and Password** values will be given to you by your instructor.

 ![](images/300/image003.png)  

 **1.1.3** You may be presented with the tutorial overlay for the ICS Service Console - since we already went through ICS in Lab 100, dismiss the tutorial by clicking on _Got It!_

 ![](images/300/image004d.png)

 **1.1.4** You will now be presented with the ICS Service Console from which you will be performing the rest of this workshop lab.

  ![](images/300/image004c.png)

 **1.2**: Check your Connections

  **1.1** From the Integration Cloud Dashboard, click on the "Connections".
  ICS console will be loaded in new window.
 If you see anything other than green checks, then go back to the previous steps

  ![](images/300/image102.png)

 **1.3**:ICS and HCM Connections

  **1.3** Now go back to the dashboard and go to the "Integrations". Click on “ICSHCM_Add Talent Profile” or search if it is not in view on the screen.

----

### ICS Development

In the top right of the Integrations page, click “Create”.

![](images/300/image300.png)

Select the “Orchestration” style/pattern.

![](images/300/image325.png)

Enter the integration name “ICSHCM Add Talent Profile_XX”, replacing "XX" with your initials. Then, click “Create”.

![](images/300/image003.png)

Now, we will edit the orchestration for this integration. The first step is to select an application that will trigger the integration. This will be the SOAP trigger "ICSHCM_SOAP_TalentProfile_Input_UserXX", which you can find by expanding "Triggers" and then "SOAP" in the right-hand side palette. Drag the copmonent to the empty "Start" block in the orchestration flow digram, as follows:

![](images/300/image323.png)

The Wizard for configuring the SOAP endpoint will appear. On the Basic Info page, enter the name "AddTalentProfileData_UserXX", as shown below, replacing "XX" with your initials. Then,  click "Next" at the top.

![](images/300/image007.png)

Next, on the Operations page, ensure that "Disable SoapAction Validation" is set to "No". Then, click "Next".

![](images/300/image008.png)

On the Headers page, ensure that the following is set to "No", and click "Next".

![](images/300/image009.png)

A summary of the new endpoint is presented. Review it and click "Done".

![](images/300/image010.png)

The orchestration flow should now look like this:

![](images/300/image011.png)

The icons in the diagram can be stretched to add space, as follows:

![](images/300/image012.png)

Next, click "Actions" in the right-hand palette to expand it, and add an "Assign" component to the orchestration, as follows.

![](images/300/image013.png)

You are prompted to name the action. Call it "AssignFileName".

![](images/300/image014.png)

Next, click the + icon to add a new variable.

![](images/300/image015.png)

Edit the "Name" field of the new variable to "fileName". Then, click the pen icon to the right.

![](images/300/image016.png)

In the "Expression" field, enter the following:

concat("TP_UserXX", fn:year-from-dateTime(fn:current-dateTime()), fn:month-from-dateTime(fn:current-dateTime()), fn:day-from-dateTime(fn:current-dateTime()), fn:hours-from-dateTime(fn:current-dateTime()), fn:minutes-from-dateTime(fn:current-dateTime()), xsd:integer(fn:seconds-from-dateTime(fn:current-dateTime())))

![](images/300/image017.png)

Please be sure to replace "XX" with your initials.

![](images/300/image018.png)

Click "Validate".

![](images/300/image019.png)

The expression is now valid and ready to use. Click "Close" in the top right.

![](images/300/image020.png)

Click "Close" again.

![](images/300/image021.png)

Next, expand "Actions" in the right-hand side palette.

![](images/300/image022A.png)

Drag and drop a Stage File from the palette and insert it into the orchestration as follows:

![](images/300/RC_image023.png)

Edit the configuration for the Stage File Action. In the Basic Info page of the Wizard, name the action "writeInputAsHDLFormat" and click "Next".

![](images/300/RC_image024.png)

On the Configure Operation page, select "Write File" from the drop-down menu, as shown below. Then, click the pen icon corresponding to "Specify the File Name".

![](images/300/RC_image025A.png)

This is the Expression Builder page. Enter the Expression "TalentProfile.dat" (with quotes) and click "Save". Then, click "OK" in the popup, followed by "Exit Expression Builder".

![](images/300/RC_image025B.png)

After returning to the main Stage File Action configuration page, click the pen icon corresponding to "Specify the Output Directory".

![](images/300/RC_image027A.png)

This time, in the expression builder, enter ".vsf" (with quotes). As before, click "Save", "OK", and "Exit Expression Builder".

![](images/300/RC_image027B.png)

Click "Next" on the Configure Operation page.

![](images/300/image027N.png)

In Schema Options, click the radio button for "Select an existing schema from the file system", as shown below. Then, click "Next".

![](images/300/RC_image028.png)

In Format Definition, click "Choose File" to open your local file explorer.

![](images/300/image030C.png)

From the provided lab artifacts folder, select the file "hcm-talentprofile.nxsd".

![](images/300/image030D.png)

In the drop-down for "Select the Schema Element", select "TalentProfileFileData" and click "Next".

![](images/300/RC_image030.png)

Here is a summary of the configuration for the Stage File Action "writeInputAsHDLFormat". Review it and click "Done".

![](images/300/RC_image031.png)

Next, in the orchestration palette, expand "Actions" and add a Stage File component as follows.

![](images/300/RC_image032.png)

Here is the configuration wizard. In the Basic Info page, name the action "zipHDLFile" and click "Next".

![](images/300/RC_image033.png)

On the Configure Operation page, select "Zip Files" from the drop-down menu, as shown below. Then, click the pen icon corresponding to "Specify the File Name".

![](images/300/RC_image034A.png)

In the Expression Builder, enter "TalentProfile.dat" (with quotes) for the expression name. Then follow the same steps as before to exit the Expression Builder.

![](images/300/RC_image025B.png)

Next, select the bottom pen icon, corresponding to "Specify the Directory to Zip".

![](images/300/RC_image035A.png)

In the Expression Builder, enter ".vsf" (with quotes), save, and exit:

![](images/300/RC_image035B.png)

Here is a summary of the configuration for the Stage File Action "zipHDLFile". Review it and click "Done".

![](images/300/RC_image037.png)

Next, expand "Invokes" in the right-side palette, followed by "FTP". Then, select "ICSHCM-POC-FTP_UserXX" and add it to the orchestration as follows: 

![](images/300/RC_image038.png)


On the Basic Info page of the Endpoint Configuration Wizard, name the endpoint "ftpSendZippedHDLFile" and click "Next".

![](images/300/RC_image040.png)

In Operations, apply the following settings and click "Next".

![](images/300/RC_image041.png)

In Schema, ensure that the radio button for "No" is selected and click "Next".

![](images/300/RC_image042.png)

Here is a summary of the configuration for the endpoint "ftpSendZippedHDLFile". Review it and click "Done".

![](images/300/RC_image043.png)

Next, expand "Invokes" and "FTP" in the palette, and add the component "ICSHCM-POC-FTP_UserXX" to the orchestration as follows: 

![](images/300/RC_image044.png)

Edit the endpoint configuration as before. In Basic Info, name the endpoint "ftpReadZippedHDLFileBase64" and click "Next".

![](images/300/RC_image045.png)

In Operations, apply the following settings and click "Next".

![](images/300/RC_image046.png)

In Schema, ensure that the radio button for "No" is selected and click "Next".

![](images/300/RC_image047.png)

In Format Definition, click "Browse" and select the file "opaque.nxsd". Ensure that the Schema Element "opaqueData" is selected and click "Next".

![](images/300/RC_image048.png)

Here is a summary of the configuration for the endpoint "ftpReadZippedHDLFileBase64". Review it and click "Done".

![](images/300/RC_image049.png)

Next, in the orchestration palette, expand "Invokes" and then "SOAP". Add "ICSHCM-POC-FA-UCM-Conn_UserXX" to the orchestration as follows:  

![](images/300/RC_image050.png)

Edit the SOAP endpoint configuration. On the Basic Info page, name the endpoint "UploadFileToUCM". Click "Next" until you reach the Summary page.

![](images/300/RC_image051.png)

Review the configuration for the endpoint "UploadFileToUCM" and click "Done".

![](images/300/RC_image052.png)

Next, in the orchestration palette, expand "Invokes" and then "SOAP", as before. This time, select "ICSHCM-POC-FA-HCM-Conn_UserXX" and add it to the orchestration as follows:

![](images/300/RC_image053.png)

Edit the configuration for this SOAP endpoint. On the Basic Info page, name the endpoint "ScheduleImportProcessHCM". Click "Next" until you reach the Summary page.

![](images/300/RC_image054.png)

In Operations, select the operation "importAndLoadData" and click "Next".

![](images/300/RC_image055.png)

Here is a summary of the configuration for the endpoint "ScheduleImportProcessHCM". Review it and click "Done".

![](images/300/RC_image056.png)

As a final step, we will configure the mapping components of the orchestration. There are six of them in total. Click on the first one ("Map to "writeInputAsHDLFormat"), as shown below.

![](images/300/RC_image061.png)

Click the pen icon to edit the mapping.

![](images/300/RC_image062.png)

On the right (Target) side of the mapping page, click the triangle next to "TalentProfile" to expand it.  

![](images/300/RC_image064.png)

Drag and drop each field (starting with "PersonNumber") from the Source side to the Target side, under "TalentProfile", as follows:

![](images/300/RC_image065.png)

After you complete all 5 fields, the mapping should look like this:

![](images/300/RC_image066.png)

Then, under Target, expand "ProfileItem".

![](images/300/RC_image067.png)

Drag and drop each field from Source to Target as before, except this time for "ProfileItem" instead of "TalentProfile". Then, click "Validate" and "Close".

![](images/300/RC_image068A.png)

Returning to the orchestration, the mapping component to "writeInputAsHDLFormat" now appears blue, showing that it is configured.

![](images/300/RC_image070.png)

Next, we will edit the second mapping: the one to "ftpSendZippedHDLFile". Click on the corresponding pen icon, as before.

![](images/300/RC_image070A.png)

On the mapping page, first drag "$fileName" from Source to Target, as shown below. Then, in the Mapping column, click the field to the right of the Target "$fileName" to edit it. 

![](images/300/RC_image071.png)

Click the pen icon to edit the statement.

![](images/300/RC_image072.png)

On the left, expand the "Mapping Components" bar under "Source". Type "concat" in the search box and click the search icon. Then, drag and drop "concat" to "$fileName", as shown below:

![](images/300/RC_image073.png)

When asked to select a parameter, choose "None" and click "OK".

![](images/300/RC_image074.png)

Collapse "Mapping" and re-expand "Source". Then, move the "fileName" element below "concat" as "string1".

![](images/300/RC_image075.png)

For "string2", enter the text '.zip' (with single quotes). This will append the file name with the correct extension.

![](images/300/RC_image076.png)

Next, we will edit the third mapping: the one to "ftpReadZippedHDLFile". Click on the corresponding pen icon.

![](images/300/RC_image078.png)

Here, note that the Mapping column has been updated to reflect your previous actions. Drag and drop the "FileReference" element as shown below. Click "Validate" save your changes and then "Close". 

![](images/300/RC_image077.png)

Next, we will edit the fourth mapping: the one to "UploadHDLFileToUCM".

![](images/300/RC_image081.png)

Apply the mapping from Source to Target in accordance with the following table and image:

![](images/300/RC_image079.png)
![](images/300/RC_image080.png)

Under Target on the right side, click "Field" and then "Repeat Element".

![](images/300/RC_image082.png)

Expand "Document" as follows:

![](images/300/RC_image083.png)

Drag and drop "fileName" from Source to Target Field 1 of 7 as follows, changing the mapping:

![](images/300/RC_image084.png)

Click "Mapping Components" to expand it.

![](images/300/RC_image085.png)

Enter "upper" in the search box and click the search icon. Drag and drop the element "upper-case" as follows. Then, click "Save" and "Close". 

![](images/300/RC_image086.png)

For Field 2 under Target, click to enter text.

![](images/300/RC_image087.png)

Enter "anonymous" and then click "Save" and "Close".

![](images/300/RC_image088.png)

For Field 3, drag and drop "fileName" from Source to Target as you did for Field 1. For Fields 4 to 7, enter the following text as you did for Field 2:

![](images/300/RC_image089.png)

Next, drag "opaqueData" to "Contents".

![](images/300/RC_image090.png)

Set "name" as "primaryFile".

![](images/300/RC_image091.png)

Drag "fileName" to "href", as follows:

![](images/300/RC_image092.png)

Expand "Mapping Components". Type "concat" in the search box and click the search icon. Drag and drop the "concat" element as follows:

![](images/300/RC_image093.png)

When prompted to select a parameter, choose "string2" and click "OK".

![](images/300/RC_image094.png)



![](images/300/RC_image095.png)
![](images/300/RC_image096.png)
![](images/300/RC_image097.png)
![](images/300/RC_image098.png)

Click "Validate" and "Close".

![](images/300/RC_image099.png)

Next, we will edit the fifth mapping: the one to "ScheduleImportProcessHCM".

![](images/300/RC_image101.png)

Drag "fileName" (Source) to "ContentId" (Target), changing the mapping, as shown below:

![](images/300/RC_image102.png)

Expand "Mapping Components" and type "upper" in the search box. Then, click the search icon. Drag the element "upper-case" as follows. Click "Save" and "Close". 

![](images/300/RC_image103.png)

Click "Validate" and then "Close".

![](images/300/RC_image104.png)

Now, we will edit the sixth and final mapping: the one to "AddTalentProfileData".

![](images/300/RC_image111.png)

Drag "result" from Source to Target as shown below. Then, click "Validate" and "Close".


----
----
----


When complete, the entire integration flow should look like this:

![](images/300/image105.png)
![](images/300/image106.png)
![](images/300/image107.png)

Next, enable tracing and click on "Activate".

![](images/300/image318.png)

Click on the info icon and note the endpoint url.

![](images/300/image319.png)

