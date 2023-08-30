
![[Pasted image 20230825172632.png]]
![[Pasted image 20230825172645.png]]
![[Pasted image 20230825172715.png]]
![[Pasted image 20230825173049.png]]

##### Lab 10
Configure Application Insights with Azure

![[1242_S05_LAB09_ConfigureApplicationInsightsWithAzure.png]]
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