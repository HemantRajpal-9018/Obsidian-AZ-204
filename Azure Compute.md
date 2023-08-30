
1.[[ARM]]
2.[[Container]]
3.[[Azure App]]

##### Lab1


![[images.jpeg]]
Deploy a Small Environment Using an ARM Template
Introduction
In this lab, you'll use the Azure Custom Template editing tool to build and deploy from an ARM template. The goal of this lab is to introduce you to how ARM templates are built and teach you how to use one of the more underrated tools in the Azure console.
Solution

Log in to the Azure portal using the credentials provided on the lab page. Be sure to use an incognito or private browser window to ensure you're using the lab account rather than your own.
Create a Basic ARM Template

1. From the top search bar, search for and select **Deploy a custom template**.
    
2. Click **Build your own template in the editor**.
    
3. Click **+ Add resource**.
    
4. From the **Select a resource** dropdown menu, select **Virtual network**.
    
5. Under **Name**, enter in a simple name, such as _acg-lab-network_.
    
6. To save the resource, click **OK**.
    
7. Click **+ Add resource**.
    
8. In the **Select a resource** dropdown menu, select **Windows virtual machine**.
    
9. Under **Name**, enter in a simple name, such as _acg-labvm_.
    
10. Under **Storage account**, define the storage account with an easy-to-remember name, such as _acgstorage_.
    
11. In the **Select from existing template** dropdown menu, select the existing network.
    
12. Click **OK**.
    
13. In the template, change the line that currently reads `acg-labvmVmsize: "Standard_D1",` to:
    
    `acg-labvmVmsize: "Standard_B1s",`
    
14. Click **Save**.
    
 Deploy the ARM Template

1. For **Resource group**, select the default resource group from the dropdown menu.
2. For the **labvm Name**, enter _labvm01_.
3. For **Admin User Name**, enter _acgadmin_.
4. Enter a value for the **Password**.
5. Leave the default OS version for the VM.
6. Click **Review + create**.
7. Click **Create** to finish creating and deploying the VM. The creation process may take a minute or two.

Verify Environment Deployed Successfully

Click **Go to resource group**. You should see all the resources that were created.

Bonus: Download a Template for Future Reuse
1. From the top search bar, search for and select **Deploy a custom template**.
2. Click **Build your own template in the editor**.
3. Click **+ Add a resource** to add a quick resource.
4. In the **Select a resource** dropdown menu, select **Virtual network**.
5. Under **Name**, enter any name.
6. Click **OK**.
7. In the top action bar, click **Download** to get a JSON file containing the template that you can reuse in the future.
Conclusion

Congratulations — you've completed this hands-on lab!

![[Pasted image 20230810193630.png]]

![[Pasted image 20230810193651.png]]





##### Lab2

![[Pasted image 20230814012205.png]]

Deploy a Container to Azure Container Instances

Introduction

For this lab, we'll perform a basic container deployment to Azure Container Instances. You'll deploy a container, verify it exists, and then remove it from Azure to ensure you know how to perform these basic operations with ease.
Solution

Log in to the Azure portal using the credentials provided on the lab instructions page.

 Deploy an Azure Container Instance (Azure Console)

1. In the search bar on top of the page, type "containers".
2. From the search results, select **Container instances**.
3. Click the **Create container instances** button.
4. On the _Basics_ tab of _Create a Front Door_, configure the following settings:

- _Resource group_: Select the existing resource group from the dropdown menu.
- _Container name_: Enter a simple name, such as "acg-lab01".
- _Image source_: Select **Quickstart images**.
- _Image_: Select the **helloworld** image from the dropdown menu.
- _Size_: Click **Change size**.
    - In the _Change container size_ pane on the right-hand side, under _Memory (GiB)_, enter "1".
    - Click **OK**.

1. Click **Next: Networking >**.
2. On the _Basics_ tab of _Create a Front Door_, configure the following settings:

- _Networking_: Keep the network type as public.
- _DNS name label_: Enter a simple name, such as "acglab00001".

1. Click **Next: Advanced >**.
2. Click **Next: Tags >**.
3. Click **Next: Review + create**.
4. Click **Create**.
5. When the container is finished deploying, click **Go to resource**.
6. Next to _FQDN_, copy the URL provided.
7. Open a new browser window or tab and copy the URL into the address bar using http.
8. Return to the Azure console.

Stop and Delete Your Containers

1. Return to the Azure container overview page.
2. Click the **Stop** icon on top to stop the container from running.
3. When prompted, click **Yes** to confirm you want to stop the container.
4. Click the **Delete** icon to delete the character.
5. When prompted, click **Yes** to confirm you want to delete the container.

Conclusion

Congratulations — you've completed this hands-on lab!



##### Lab3

Use Azure App Service Deployment Slots with Azure CLI
Description

Azure App Service includes deployment slots that help to improve the way in which updates to your code can be deployed to production.

In this hands-on lab, we'll use Azure CLI within the Cloud Shell, in order create and use deployment slots for a simple web application.

The Cloud Shell includes Azure CLI and the .NET Core CLI, which we will use to perform all tasks.

**Scenario** You've recently been employed as a cloud developer, and have been asked to perform a proof of concept using Azure App Service deployment slots.

In order to perform this proof of concept, you will need to:

- Deploy a simple .NET Core web application to a new Web App in Azure App Service
- Make changes to your web application, and deploy these to a staging slot
- Perform a slot swap, so that your changes are promoted to production

Objectives

Successfully complete this lab by achieving the following learning objectives:

Set up a .NET Core Web App in Azure App Service

Use the below commands in Cloud Shell (Bash) for guidance:

1. Create a new demonstration web application: `dotnet new webapp`
2. Build the web application: `dotnet build`
3. Create and deploy your web app: `az webapp up -n APPNAME -g RESOURCEGROUP --sku s1`

Update your App and Upload to a Staging Slot

Use the below commands in Cloud Shell (Bash) for guidance:

1. Update your application, for example: `code Pages/Index.cshtml`
2. Create a staging slot: `az webapp deployment slot create --name APPNAME -g RESOURCEGROUP --slot staging`
3. Deploy to the staging slot:

a) Publish the updated code: `dotnet publish -o pub` b) Zip for deployment: `cd pub; zip -r webapp.zip .` c) ZipDeploy to the staging slot: `az webapp deployment source config-zip --name APPNAME --resource-group RESOURCEGROUP --src webapp.zip --slot staging`

Swap Staging and Production Slots

Use the below commands in Cloud Shell (Bash) for guidance:

1. Swap staging to production: `az webapp deployment slot swap -n APPNAME -g RESOURCEGROUP --slot staging --target-slot production`


![[6041_HOL_Using_Azure_App_Service_Deployment_Slots_-_Diagram-1.png]]




##### Lab4
![[Azure-LearningActivity-LinuxWebApps.png]]
Using Azure Web Apps with Containers, Linux, and Cloud Shell

Introduction

In this lab, you will gain experience using the Azure Cloud Shell to create App Service plans using Linux, and web apps that use Docker containers.

You will use the Azure Cloud Shell to create a Linux App Service plan, and a web app under that plan which uses Docker images on DockerHub and GitHub. When you're finished, you will browse to your site to see everything running, and will verify all the resources you created using the Azure Portal.

Getting Started

Log in to the Azure Portal using the credentials and link provided in the _Credentials_ section on the hands-on lab page.

Use Cloud Shell to Create and Update Linux App Service Plans and Web Apps

Use Cloud Shell to Create a Linux App Service Plan

Right-click the Azure Portal tab in your browser and choose the **Duplicate Tab** option. In this new tab, open the **Azure Cloud Shell** using the icon in the top menu.

Choose **PowerShell** when you are prompted. For our storage options, choose **Show advanced settings**.

Ensure that the following fields are provided for the advanced settings:

- _Cloud Shell region_: **Use the same region as the existing storage account**
- _Storage Account_: Click **Use existing**
- _File Share_: Click **Create new** and use any random name

With these options configured, click **Create Storage**.

Copy the PowerShell commands below and paste them into your Cloud Shell window:

`$resourceGroup = az group list --query '[0].name' -otsv $appServicePlan = 'Linux-App-ServicePlan' az appservice plan create -g $resourceGroup -n $appServicePlan --is-linux --number-of-workers 1 --sku B1`

Use Cloud Shell to Create a Web App Using a DockerHub Container Image

Copy the PowerShell commands below and paste them into your Cloud Shell window:

`$app = 'LinuxDockerApp' + (Get-Date).ticks az webapp create --resource-group $resourceGroup --plan $appServicePlan --name $app --deployment-container-image-name mcr.microsoft.com/dotnet/samples:aspnetapp`

Use Cloud Shell to Update a Web App Container Image from DockerHub to GitHub

Copy the PowerShell command below and paste it into your Cloud Shell window:

`az webapp config container set --resource-group $resourceGroup --name $app --docker-registry-server-url 'https://github.com/dotnet/dotnet-docker/tree/master/samples/aspnetapp'`

We can verify that this command ran successfully by navigating back to the Azure Portal. Go to your All Resources section of the Azure Portal. Select the App Service named LinuxDockerApp[some numbers]. In the Settings section, click Configuration. In the Application settings tab, you'll see 'DOCKER_REGISTRY_SERVER_URL.' Click the text 'Hidden value. Click to show value.' If you make the value column view larger, you'll see the same URL we provided in our command.

We can verify that our site is running by clicking **Overview** in the App Service menu. Our endpoint is shown in the _URL_ section on this page. Click on this URL to load our app and verify that it is running. Note: the web site has changed from what is shown in the video.

Conclusion

Congratulations on completing this hands-on lab!
##### Lab5

![[Pasted image 20230814015716.png]]
![[1242_S02_LAB04_DeployAndRunYourFirstAzureFunction.png]]
Imagine you need to regularly download and process a public dataset of physicians, but the naming convention of the file is not strictly enforced, requiring frequent human intervention to retrieve the most recent file from a link on a website. Further, the posting date of the monthly file is inconsistent, so you need to be able to check for the most current file name so that downstream processes can determine when a refresh is appropriate. The rest of your workflow is already automated; you just need to add a custom application to sort out the file name to fully automate the integration pipeline.

This is one kind of challenge that Azure Functions was designed to address. You will first learn how to provision a Function App, then create and test a canned C# .NET function in that app using an HTTP trigger template. After testing the canned function, you will modify its configuration and C# code to scrape a government website. The goal will be to retrieve the URL of the latest monthly file containing U.S. physicians and their national identifiers. The URL string will be returned for further processing by a data pipeline.

#### Summary Azure Compute
![[Pasted image 20230816172400.png]]
![[Pasted image 20230816172425.png]]
![[Pasted image 20230816172449.png]]
![[Pasted image 20230816172536.png]]
![[Pasted image 20230816172554.png]]
![[Pasted image 20230816172629.png]]
![[Pasted image 20230816172655.png]]
![[Pasted image 20230816172711.png]]
![[20230816-2127-40.8295124.mp4]]




##### Lab6

Provision a Cosmos DB Instance in Azure

Introduction

In this hands-on lab, you will learn how to provision and configure a Cosmos DB instance in the Azure portal
Solution

Log in to the Azure portal using the credentials provided on the lab instructions page.

Create a Cosmos DB Instance in the Azure Portal

1. From the Azure dashboard, type "Cosmos DB" in the search bar located at the top of the page.
2. Choose **Azure Cosmos DB** from the dropdown.
3. Click **Create Azure Cosmos DB account**.
4. Under **Azure Cosmos DB for NoSQL**, click **Create**.
5. On the **Azure Cosmos DB for NoSQL** page, configure the following settings:
    - **Resource Group**: Select the existing provisioned resource group.
    - **Account Name**: Enter a unique name.
    - **Location**: Select **(US) West US**.
    - **Capacity mode**: Select **Provisioned throughput**.
    - **Apply Free Tier Discount**: Select **Do Not Apply**.
    - **Account Type**: Select **Non-Production**.
    - **Geo-Redundancy**: Select **Enable**.
    - **Multi-region Writes**: Select **Enable**.
6. Click **Review + create** tab, located near top of the page.
7. Click **Create**.

Configure Cosmos DB

1. Once the deployment is complete, click **Go to resource**.
2. In the left navigation menu, click **Replicate data globally**.
3. Locate the **South Central US** region on the world map, and click the corresponding circle on the map to select it.
4. Click **Save**.
5. Wait for the region configuration operation to complete.
6. In the left navigation menu, click **Default consistency**.
7. Select **EVENTUAL**.
8. Click **Save**.
9. Wait until the consistency configuration operation is complete.
10. In the left navigation menu, click **Quick start**.
11. Click **Create 'Items' container**.
12. Click **Open Data Explorer**.
13. Under **Data**, click **ToDoList** > **Items** > **Scale & Settings**.
14. Under **Indexing Policy**, locate the `indexingMode` parameter in line #2, and change its value from `consistent` to `none`.
15. Delete lines #3 - #13, as well as the comma after `none`, and the remaining syntax should be:
    
    `{ "indexingMode": "none" }`
    
16. Click **Save**.
17. In the left navigation menu under **Monitoring**, click **Alerts**.
18. Click **Create alert rule**.
19. Search and select **Provisioned Throughput**.
20. Set the following values:
    - **Aggregation Type**: Select **Maximum**.
    - **Operator**: Select **Less than**.
    - **Unit**: Select **Count**.
    - **Threshold value**: Type _50_.
    - **Lookback period**: Select **5 minutes**.
    - **Check every**: Select **1 minute**.
21. Click **Next**.
22. Click **+ Create action group**.
23. Set the **Action group name** to any unique name.
    
 Note: The **Display name** will only display the first 12 characters.
    
24. Click **Notifications**, and set the following values:
    - **Notification Type**: Select **Email/SMS message/Push/Voice**.
    - **Name**: Enter a unique name.
    - **Email**: Click to check box and enter an email address.
25. Click **OK**.
26. Click **Review + create**.
27. Click **Next: Details**.
28. Under **Severity**, select **2 - Warning**.
29. Under **Alert rule name**, enter a unique name.
30. Click **Review + create**.
31. Click **Create**.
32. Click **Alert rules** to confirm existence of the created rule.

Conclusion
Congratulations, you've successfully completed this hands-on lab!

##### Lab6

![[Provision a Cosmos DB Instance in Azure - Diagram.png]]
Provisioning a Cosmos DB Instance in Azure
 Introduction

In this hands-on lab, you will learn how to provision and configure a Cosmos DB instance in the Azure portal.

 Solution

Log in to the Azure portal using the credentials provided on the lab instructions page.

Create a Cosmos DB Instance in the Azure Portal

1. From the Azure dashboard, type "Cosmos DB" in the search bar located at the top of the page.
2. Choose **Azure Cosmos DB** from the dropdown.
3. Click **Create Azure Cosmos DB account**.
4. Under **Azure Cosmos DB for NoSQL**, click **Create**.
5. On the **Azure Cosmos DB for NoSQL** page, configure the following settings:
    - **Resource Group**: Select the existing provisioned resource group.
    - **Account Name**: Enter a unique name.
    - **Location**: Select **(US) West US**.
    - **Capacity mode**: Select **Provisioned throughput**.
    - **Apply Free Tier Discount**: Select **Do Not Apply**.
    - **Account Type**: Select **Non-Production**.
    - **Geo-Redundancy**: Select **Enable**.
    - **Multi-region Writes**: Select **Enable**.
6. Click **Review + create** tab, located near top of the page.
7. Click **Create**.

Configure Cosmos DB

1. Once the deployment is complete, click **Go to resource**.
2. In the left navigation menu, click **Replicate data globally**.
3. Locate the **South Central US** region on the world map, and click the corresponding circle on the map to select it.
4. Click **Save**.
5. Wait for the region configuration operation to complete.
6. In the left navigation menu, click **Default consistency**.
7. Select **EVENTUAL**.
8. Click **Save**.
9. Wait until the consistency configuration operation is complete.
10. In the left navigation menu, click **Quick start**.
11. Click **Create 'Items' container**.
12. Click **Open Data Explorer**.
13. Under **Data**, click **ToDoList** > **Items** > **Scale & Settings**.
14. Under **Indexing Policy**, locate the `indexingMode` parameter in line #2, and change its value from `consistent` to `none`.
15. Delete lines #3 - #13, as well as the comma after `none`, and the remaining syntax should be:
    
    `{ "indexingMode": "none" }`
    
16. Click **Save**.
17. In the left navigation menu under **Monitoring**, click **Alerts**.
18. Click **Create alert rule**.
19. Search and select **Provisioned Throughput**.
20. Set the following values:
    - **Aggregation Type**: Select **Maximum**.
    - **Operator**: Select **Less than**.
    - **Unit**: Select **Count**.
    - **Threshold value**: Type _50_.
    - **Lookback period**: Select **5 minutes**.
    - **Check every**: Select **1 minute**.
21. Click **Next**.
22. Click **+ Create action group**.
23. Set the **Action group name** to any unique name.
    
  Note: The **Display name** will only display the first 12 characters.
    
24. Click **Notifications**, and set the following values:
    - **Notification Type**: Select **Email/SMS message/Push/Voice**.
    - **Name**: Enter a unique name.
    - **Email**: Click to check box and enter an email address.
25. Click **OK**.
26. Click **Review + create**.
27. Click **Next: Details**.
28. Under **Severity**, select **2 - Warning**.
29. Under **Alert rule name**, enter a unique name.
30. Click **Review + create**.
31. Click **Create**.
32. Click **Alert rules** to confirm existence of the created rule.
Conclusion

Congratulations, you've successfully completed this hands-on lab!
