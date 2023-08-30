##### Lab 6
**Provisioning a Cosmos DB Instance in Azure**
![[Provision a Cosmos DB Instance in Azure - Diagram 1.png]]

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

##### Lab7

Interact with Azure Blobs Using REST
![[03_LAB03_interacting_with_azure_blobs_using_rest.png]]

Introduction

Azure provides a variety of ways to interact with Blob storage. You can manage and access Blob storage using the Azure portal, a command line, or your own custom code. In this hands-on lab, you will have the opportunity to work with Azure storage using the Azure Blob Service REST API. Using basic HTTP requests, you will download some data stored in a Blob, modify it, and re-upload the modified data to the Blob.

Solution

1. Log in to the Azure portal using the credentials provided on the lab instructions page.
2. Open the provided lab-VM instant terminal.

Authenticate with the Azure Blob Service REST API and Download the File

1. Log in to the lab VM provided with this lab:
    
    `ssh cloud_user@{INSERT PUBLIC IP ADDRESS OF LAB VM}`
    
2. If prompted to accept the key, type "yes".
    
3. Enter the provided password for the lab VM.
    
4. Set up temporary environment variables to make it easier to utilize the REST API, starting with the date:
    
    `request_date=$(TZ=GMT date "+%a, %d %h %Y %H:%M:%S %Z")`
    
5. Set the storage service version number for the storage service we are using:
    
    `storage_service_version="2015-04-05"`
    
6. Return to the page where you have the Azure portal open.
    
7. In the list of resources, click the name of the item with the type _Storage account_.
    
8. Copy the storage account name at the top of the page. The name should start with "sattrecords".
    
9. Return to the terminal.
    
10. Set the storage account name as an environment variable:
    
    `storage_account="INSERT YOUR STORAGE ACCOUNT NAME"`
    
11. Return to the page where you have the Azure portal open.
    
12. In the left-hand navigation menu, under _Settings_, click **Access keys**.
    
13. Copy the key listed under _Key_ in _key1_.
    
14. Return to the terminal.
    
15. Set the access key:
    
    `access_key="INSERT YOUR STORAGE ACCOUNT ACCESS KEY"`
    
16. Set the resource environment variable for the Blob that contains our Blob data:
    
    `resource="/${storage_account}/records/cars"`
    
17. Set the request method environment variable:
    
    `request_method="GET"`
    
18. Start generating an authorization header to authenticate with our REST API by first setting an environment variable to a list of headers:
    
    `headers="x-ms-date:$request_date\nx-ms-version:$storage_service_version"`
    
19. Create an environment variable that contains the string that will be signed with our signature:
    
    `string_to_sign="${request_method}\n\n\n\n\n\n\n\n\n\n\n\n${headers}\n${resource}"`
    
20. Create a variable that stores and decodes the access key and converts it to hex:
    
    `hex_key="$(echo -n $access_key | base64 -d -w0 | xxd -p -c256)"`
    
21. Generate the signature using the environment variables we have created:
    
    `signature=$(printf "$string_to_sign" | openssl dgst -sha256 -mac HMAC -macopt "hexkey:$hex_key" -binary | base64 -w0)`
    
22. Generate the authorization header using the signature we just generated:
    
    `authorization_header="SharedKey $storage_account:$signature"`
    
23. Make an HTTP request to the REST API to download the Blob data to a local file:
    
    `curl -H "x-ms-date:$request_date" \ -H "x-ms-version:$storage_service_version" \ -H "Authorization: $authorization_header" \ "https://${storage_account}.blob.core.windows.net/records/cars" > cars.csv`
    
24. Verify that the local file contains the Blob data:
    
    `cat cars.csv`
    

 Authenticate with the Azure Blob Service REST API and Download the File

1. To add new data to the local `cars.csv` file, open the file for editing:
    
    `vi cars.csv`
    
2. Reach the end of the file and add a new line by typing "i" to enter Insert mode, followed by capital letter "O" to insert a new line.
    
3. Copy the following new customer record to the new line at the end of the file:
    
    `57991237,2020,Tesla,Cybertruck,X3B-33`
    
4. Save and quit the file by pressing the Escape key and entering the following:
    
    `:wq`
    
5. Reset the `request_date` environment variable to the current timestamp:
    
    `request_date=$(TZ=GMT date "+%a, %d %h %Y %H:%M:%S %Z")`
    
6. Change the request method to a PUT rather than a GET:
    
    `request_method="PUT"`
    
7. Set the content type as an environmental variable:
    
    `content_type="text.plain"`
    
8. Obtain the length of the local file and store it as an environmental variable:
    
    `file_length=$(wc -m < cars.csv)`
    
9. Generate a new set of authorization headers:
    
    `headers="x-ms-blob-type:BlockBlob\nx-ms-date:$request_date\nx-ms-version:$storage_service_version"`
    
10. Generate a new string to sign environmental variable:
    
    `string_to_sign="${request_method}\n\n\n$file_length\n\n$content_type\n\n\n\n\n\n\n${headers}\n${resource}"`
    
11. Generate a new signature based on all the new variables:
    
    `signature=$(printf "$string_to_sign" | openssl dgst -sha256 -mac HMAC -macopt "hexkey:$hex_key" -binary | base64 -w0)`
    
12. Set your authorization header again:
    
    `authorization_header="SharedKey $storage_account:$signature"`
    
13. Make a new HTTPS request to the REST API to upload the new data to the Blob:
    
    `curl -X PUT -H "x-ms-blob-type:BlockBlob" \ -H "x-ms-date:$request_date" \ -H "x-ms-version:$storage_service_version" \ -H "Authorization: $authorization_header" \ -H "Content-Length:$file_length" \ -H "Content-Type:$content_type" \ --data-binary "@cars.csv" \ "https://${storage_account}.blob.core.windows.net/records/cars"`
    
14. To visually verify that your changes were made, return to the Azure portal.
    
15. In the left-hand navigation menu, under _Blob service_, click **Containers**.
    
16. Click the **records** container.
    
17. Click the **cars** Blob.
    
18. Click the **Edit** tab. At the end of the list should be the Tesla Cybertruck line.
    

Conclusion

Congratulations — you've completed this hands-on lab!
