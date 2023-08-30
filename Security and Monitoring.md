
![[Pasted image 20230818205004.png]]
![[Pasted image 20230818205041.png]]
![[Pasted image 20230818205119.png]]
![[Pasted image 20230818205145.png]]

1. [[Azure App Configuration]]
2. **Feature Flags**
![[Pasted image 20230821182337.png]]
![[Pasted image 20230821182402.png]]
3. **Managed Identity**
![[Pasted image 20230825153509.png]]
4. [[Azure Monitor]]
5. [[Application Insights]]
6. [[Review]]
##### Lab 8

Configuration and Security of Azure Storage Accounts
![[1060_-_S11-HOL_-_Configuration_and_Security_of_Azure_Storage_Accounts.001.png]]


Guided Mode

2 hours duration

Practitioner

Video 1 of 5

Introduction

This video introduces the scenario for the learning activity and covers the steps we need to take to complete it.

Tools
Description

This hands-on lab provides some experience with configuring and securing an Azure storage account. We log in to the Azure portal and create a storage account, and then get familiar with the configuration options for it, including replication options, access tiers, and secure transfers. We RDP into a Windows VM and use Microsoft Azure Storage Explorer to connect to the storage account. We use Blob storage and attempt to upload and retrieve data from the blob. Using the Azure portal, we use access policies and shared access signatures to both permit access to the storage account and deny access to blob data. Subsequent attempts to upload and retrieve data from Blob storage should fail. Completing the lab provides the experience required to configure and secure an Azure storage account.

Objectives

Successfully complete this lab by achieving the following learning objectives:

Create and Configure a Storage Account

1. In the Azure portal, click **Create**.
2. In the search bar, type and select **Storage account**.
3. Click **Create**.
4. Create a storage account in the current resource group.

Log In to the VM with RDP

Log in to the virtual machine that was provisioned for this lab using the username/password provided in the lab credentials.

**Note:** There may be an issue with the **Connect** option in the Azure portal. If this occurs for you, you can still RDP using your favorite RDP client and the public IP address of the VM.

Open Azure Storage Explorer, Connect to the Azure Account, and Upload Image Files

1. In the VM, open Azure Storage Explorer and connect to the Azure account using the provided credentials.
2. Create a new Blob Storage container and upload sample images to the storage account using the files stored in `C:\images` on the VM.

Upload Storage Account Files in Azure Storage Explorer Using Access Keys and Revoke Storage Account Access

1. In the Azure portal, copy the `key1` access key for the Storage Account.
2. Within Azure Storage Explorer, connect to the Storage Account using the `key1` access key.
3. Upload images to the `images` container.
4. In the Azure portal, rotate the `key1` access key.
5. In Azure Storage Explorer on the virtual machine, refresh the connection and attempt to view the containers.

##### Lab 9
Limit Access to Azure Storage Account Using SAS URI

![[1242_S04_LAB07_LimitAccessToAzureStorageAccountUsingSASURI.png]]
Introduction

In this lab, you will have an opportunity to create a SAS token for access to an Azure Storage account and then test the SAS-based access by working with the storage account from a separate environment. Students with at least some Azure experience will have the best opportunity to complete the lab without assistance, but the lab guide and solution videos provide a full walkthrough if you get stuck.

Solution

Log in to the Azure portal using the credentials provided on the lab page. Be sure to use an incognito or private browser window to ensure you're using the lab account rather than your own.

Create two sample text files for use later in the lab. Save them to your Desktop or a location you can easily access.

Prepare Testing Environment

Connect to RDP

Use the Remote Desktop client

1. From the **Resources** list of the resource group **Overview** page, click the listed **vm** virtual machine.
2. Click **Connect**.
3. Click **Download RDP File**.
4. Open the file in your Remote Desktop app.
5. Log in to the virtual machine using the following credentials:
    - **User Name**: Enter _cloud_user_.
    - **Password**: Use the password for the **vm** found in your lab credentials.
6. If you are prompted to make your VM discoverable, click **Yes**. If the **Server Manager** appears, close it.

Install and Configure Azure Storage Explorer

1. Open the **Edge** browser. Navigate through the browser setup prompts.
2. From Edge, download the [Azure Storage Explorer](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) software on the VM.
    - On the Azure Storage Explorer web page, click the **Operating system** button, and select **Windows**.
    - Once the file is downloaded, open it to initiate the installation process.
3. Follow all the installation prompts, including accepting license agreements. It may take a few minutes to install.
4. Once the installation process is complete, ensure **Launch Microsoft Azure Storage Explorer** is checked, and click **Finish**. The Explorer will start up in a new window.
5. From Azure Storage Explorer, click **Attach to a resource**.
6. On the **Select Resource** dialog page, select **Storage account or service**.
7. On the **Select Connection Method** dialog page, select **Shared access signature URL (SAS)** for how you will connect to the storage account. Then, click **Next**.
8. On the **Enter Connection Info** dialog page, for **Display name**, enter _MyLabCnx_.

Prepare Two Text Files and a Container

1. Minimize your RDP session, **but don't log out of or close it**. Go back to the Azure portal.
2. You should still be on the RDP screen. Use the breadcrumb navigation to go back to the resource group.
3. From the **Resources** list, click the link for the **Storage account** that was pre-provisioned for you. (It begins with **pslab**.)
4. From the left navigation pane, under **Data storage**, select **Containers**.
5. Click **+ Container**.
6. In the **New container** pop-up, enter _container1_ for **Name**.
7. Click **Create**. Then, select the new container from the list to open it.
8. Upload the two text files you created at the beginning of the lab. If you did not create them, create two sample files now, and click **Upload** to upload them.

Create and Test a SAS Token

Create the SAS Token

1. Click the last link in the breadcrumb navigation to go back to the storage account.
2. From the left navigation, under **Settings**, click **Configuration**.
3. Change the **Allow storage account key access** setting to **Enabled**.
4. Click **Save**.
5. In the left navigation menu, scroll up to the **Security + networking** section, and click **Shared access signature**.
6. On the **Shared access signature** page, configure the following settings:
    - For **Allowed services**, ensure only **Blob** is checked.
    - For **Allowed resource types**, select **Service**, **Container**, and **Object**.
    - For **Allowed permissions**, select only **Read** and **List**.
    - For **Allowed protocols**, ensure only **HTTPS only** is selected.
7. Click **Generate SAS and connection string**.

Test the Token

1. Copy the generated **Blob service SAS URL**. Paste it to a secure location, as this URL is displayed only one time.
2. Go back to the RDP session. Paste the copied token to the **Service URL** box. Then, click **Next**.
3. Click **Connect**.
4. Look for **MyLabCnx** to show up in the Explorer pane of Storage Explorer.
5. Expand **MyLabCnx** > **Blob Containers**, and then double click **container1**.
6. You should see both items that you uploaded. Try deleting a file:
    - Select a file from the list.
    - Click **More** > **Delete** > **Yes**.
    - Observe in the **Activities** section that the delete action fails. This is based on the permissions you set. The only actions you should be able to complete are to see a list of available blobs and read the blobs.

Conclusion
Congratulations — you've completed this hands-on lab!










##### Lab 10
Configure Application Insights with Azure
![[1242_S05_LAB09_ConfigureApplicationInsightsWithAzure 1.png]]

Introduction

Application Insights can assist you in determining the availability and performance of your web applications. In this lab, you deploy Application Insights into the Azure lab environment and use it to run a URL ping test against the sample web app.

Solution

Log in to the Azure portal using the credentials provided on the lab page. Be sure to use an incognito or private browser window to ensure you're using the lab account rather than your own.

Verify the Existence of Azure Resources

1. If you do not land in the resource group, click on **All Resources** in the navigation menu to view the provisioned resources.
2. Survey the resources already provisioned in the resource group overview page: an App Service plan, a web app, and a Log Analytics workspace.
3. Click the link that begins with the prefix `webapp` for the **App Service** resource.
4. In the upper left corner, right-click **Browse**, copy the link for the URL to your clipboard, and save it in a text file for later.
5. Click **Browse** to preview the website.

Configure Application Insights for the Azure Web App

1. In the left navigation menu, under **Settings**, click **Application Insights**.
2. Click **Turn on Application Insights**.
3. Under **Log Analytics Workspace**, click on the dropdown menu and select the existing Log Analytics workspace; it will correspond with the name of the Azure web app (i.e., not the `new` one).
4. Under **Instrument your application**, select **.NET**.
5. Under **Collection level**, choose **Basic**.
6. Click **Apply**; then, click **Yes**.

Create and Configure the URL Ping Test

1. Once it's deployed, in the upper left breadcrumb trail, click on the resource group.
2. In the top toolbar, click on the **Refresh** icon; you should see the new Application Insights instance.
3. Click on that new Application Insights instance.
4. In the left navigation menu, under **Investigate**, click **Availability**.
5. In the top toolbar, click **+ Add Classic test**.
6. In the right **Create test** pane, Enter _URLTest1_ for the **Test name**.
7. Ensure the **SKU** is **URL ping**.
8. Under **URL**, paste in the URL you copied in objective 1.
9. Click **Create**.
10. Once it's created, you should see it under **Availability Test**.
11. Click the **...** at the end of the `URLTest1` row.
12. Select **Open Rules (Alerts) page**.

Create Action Group

1. In the **Rules** pane, click the link to open the rule.
2. In the upper right corner, click **Edit**.
3. Scroll down and, under **Actions**, click **Select action groups**.
4. In the right **Select action groups** pane, click **+ Create action group**.
5. In the **Basics** tab, under **Instance details** > **Action group name**, enter _ActionGroup1_.
6. Click **Next: Notifications**.
7. Under **Notification type**, click on the dropdown menu and select **Email/SMS message/Push/Voice**.
8. For the **Name**, enter _EmailMe_.
9. On the right-hand pane, click the checkbox next to **Email** to select it.
10. Enter your email address in the **Email** field.
11. Click **OK**.
12. Click **Review + create**.
13. Click **Create**.
14. Check your email account to verify you've received a notification about being added to the action group.
15. Click **Save** in the upper left corner.
16. In the upper left breadcrumb trail, click on the Azure Insights instance.
17. In the top toolbar, click on the **Refresh** icon.
18. Under **Availability Test**, click on `URLTest1` to expand the ping test; you should see 100% availability.

Cause an App Service Failure

1. In the upper left breadcrumb trail, click on the resource group.
2. Click the link for the **App Service** resource.
3. In the top toolbar, click **Stop**.
4. On the **Stop web app** pop-up, click **Yes**.
5. Navigate back to the browser tab previewing the website, and refresh the page; you should see `Error 403`.
6. Back in the Azure portal, in the upper left breadcrumb trail, click on the resource group.
7. Click the link for the **Application Insights** resource.
8. In the left navigation menu, under **Investigate**, click **Availability**.
9. Under **Availability Test**, click on `URLTest1` to expand the ping test.
10. In the top toolbar, click on the **Refresh** icon until multiple locations indicate an error. This may take up to five minutes.

Wait for Alert Email

Check your email and refresh your mailbox until you receive the alert email regarding the availability test failure.

Conclusion

Congratulations — you've completed this hands-on lab!





