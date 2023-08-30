
![[Pasted image 20230825195438.png]]

![[Pasted image 20230825195417.png]]

![[Pasted image 20230825195626.png]]

![[Pasted image 20230825200110.png]]
![[Pasted image 20230825200238.png]]

![[Pasted image 20230825200303.png]]
![[Pasted image 20230825200329.png]]
![[Pasted image 20230825200415.png]]
![[Pasted image 20230825200812.png]]
![[Pasted image 20230825200620.png]]
![[Pasted image 20230825200705.png]]
![[Pasted image 20230825200724.png]]

##### Lab 11

![[526_HOL_Configuring_Azure_Front_Door_Service_(CC_Diagram).png]]

Configure Azure Front Door Service

Introduction

The Azure Front Door service facilitates high availability on a global scale for web applications.

Within this hands-on lab, you will have the opportunity to create and configure the Azure Front Door service with Azure Web Apps.

Solution

Use the [Azure Portal](https://portal.azure.com) to perform the following tasks. Please log in with the credentials provided to you for this lab.

Please take note of the region in use for all of the resources that have been deployed for you, as we will need to use the same region in the following steps.

Configure Azure Front Door

1. In the Azure portal, under _Azure services_, click on **+ Create a resource** icon.
2. In the search bar, enter "front door".
3. From the search results, choose the **Front Door and CDN profiles** option.
4. Click on **Create**.
5. On the **Compare offerings** page, choose "Explore other offerings" and "Azure Front Door (classic)," then click Continue.
6. On the _Basics_ tab of _Create a Front Door_, configure the following settings:

- _Subscription:_ Select the existing subscription from the dropdown menu.
- _Resource group:_ Select the existing resource group from the dropdown menu.

1. Click **Next: Configuration >**.
2. On the _Configuration_ tab, click the plus icon next to **Frontends/domains**.
3. In the _Add a frontend host_ pane that opens up to the right, configure the following settings:

- _Host name:_ Use a unique name (e.g., fdlab1234 or fdlab001).
- _Session Affinity:_ Leave as Disabled.
- _Web Application Firewall:_ Leave as Disabled.

1. Click **Add**.
2. On the _Configuration_ tab, click the plus icon next to **Backend pools**.
3. In the _Add a backend pool_ pane that opens up to the right, configure the following settings:

- Under _Name_, enter "webapp-pool".
- Click **+ Add a backend**.
- Under _Backend host type_, select **App service**.
- Under _Host name_, choose the first web app.
- Leave the remaining settings as default.
- Click **Add**.
- To add another backend, click **+ Add a backend** again.
- Under _Backend host type_, select **App service**.
- Under _Host name_, choose the second web app.
- Leave the remaining settings as default.
- Click **Add**.

1. At the bottom of _Add a backend pool_, click **Add**.
2. On the _Configuration_ tab, click the plus icon next to **Routing rules**.
3. In the _Add a rule_ pane that opens up to the right, configure the following settings:

- Under _Name_, type "default-route".
- Under _Accepted protocol_, select **HTTP and HTTPS**.
- Under _Frontends/domains_, select your frontend.
- Under _Backened pool_, select **webapp-pool**.
- Leave all other settings as default.
- Click **Add**.

1. Click on **Review + create**.
2. Once the validation is complete, click **Create**.
Test the Azure Front Door

1. Once your deployment is complete, click on **Go to resource**.
2. Click on **Overview** in the resource menu on the left-hand side.
3. Copy on the link next to _Frontend host_ to your clipboard.
4. Click the link next to _Frontend host_. This should open a standard Python web app page in a new browser tab.
5. Return to the resource page in Azure.
6. Click on the **Home** link in the top left corner.
7. Click on the **App Services** icon in the Azure Portal.
8. Click the checkbox next to the second web app in the list.
9. Click the **Stop** button.
10. Click **Yes** to confirm.
11. To confirm that stopping the app worked, close the other two browser tabs.
12. Open a new browser tab and paste in the link to the frontend host from earlier. It should continue to work.
13. Return to the _App Services_ page.
14. Click the checkbox next to the first web app in the list.
15. Click the **Stop** button.
16. Click **Yes** to confirm.
17. Open a new browser tab and paste in the link to the frontend host from earlier. It should now fail and give an error message instead.

Conclusion

Congratulations — you've completed this hands-on lab!

**Review**
![[Pasted image 20230825202620.png]]
![[Pasted image 20230825202634.png]]



