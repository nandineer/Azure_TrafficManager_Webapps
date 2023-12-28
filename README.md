![image](https://github.com/nandineer/Azure_TrafficManager_Webapps/assets/22636122/0591b645-ca71-4c22-b917-d71c37b701bc)

**View the Pre-Created App Service Websites**

    •	In the Azure portal, inside the resource group that has been provisioned for the lab, observe the site1-xxxxx and site2-xxxxx App Service web app resources (where xxxxx will be a string of characters unique to your provisioned resources).
    •	Note the location of these two App Service web app resources, as you will need to use them later on in this lab.
    •	Open the site1-xxxxx web app resource in a new browser window or tab.
    •	On the site1 resource's Overview page, under Essentials, click the link in the URL field.
    •	Once the website launches, Site 1 text displays.
    •	Navigate back to the Azure portal Home page and open the site2-xxxxx web app resource in a new browser window or tab.
    •	On the site2 resource's Overview page, under Essentials, click the link in the URL field.
    •	Once the website launches, Site 2 text displays.
    •	You can close the browser windows/tabs where the websites launched, but keep the windows/tabs with the site1 and site2 resources open for use later on in this lab.
    
**Create a Traffic Manager Profile**

    •	Navigate back to the Azure portal Home page and, in the Search bar at the top of the window, type traffic manager and select Traffic Manager profiles from the populated list.
    •	On the Traffic Manager page, from the menu at the top, click + Create.
    •	On the Create Traffic Manager Profile page, set the following (leaving anything not specified at the default settings):
    •	Name: enter a unique name, such as xx-trafficmanager (where xx is your first and last initials)
    •	Routing method: Performance
    •	Subscription: leave the default lab subscription selected
    •	Resource group: select the resource group that has been provisioned for this lab
    •	Note: The resource group will contain the lab's title in the name.
    •	Click Create.
    •	Once the Traffic Manager profile has been deployed, click the profile resource to open it.
    •	Note: The resource will have the unique name you entered when you created it, such as xx-trafficmanager. If you don't see the profile, click the Refresh button from the menu at the top to refresh the list of resources.
    •	If necessary, click the << icon at the top of the screen to hide the Load balancing | Traffic Manager page and expand the profile page.
    •	In the navigation menu on the left, under Settings, click Configuration.
    •	On the Configuration page, scroll down to the Fast endpoint failover settings section and set the following:
    •	Probing interval: 10
    •	Tolerated number of failures: 1
    •	Probe timeout: 5
    •	From the menu at the top, click Save.
    
**Add App Service Endpoints**

    •	In the navigation menu on the left, under Settings, click Endpoints.
    •	On the Endpoints page, from the menu at the top, click + Add.
    •	In the Add endpoint pane that opens on the right, set the following to add the site1 App Service web app as an endpoint:
    •	Type: Azure endpoint
    •	Name: site1-endpoint
    •	Target resource type: App Service
    •	Target resource: select the site1-xxxxx App Service web app
    •	Click Add.
    •	From the menu at the top, click + Add again.
    •	In the Add endpoint pane that opens on the right, set the following to add the site2 App Service web app as an endpoint:
    •	Type: Azure endpoint
    •	Name: site2-endpoint
    •	Target resource type: App Service
    •	Target resource: select the site2-xxxxx App Service web app
    •	Click Add.
    •	Once the endpoints have been added and the profile changes have been saved, in the navigation menu on the left, click Overview.
    •	Under Essentials, copy the Traffic Manager profile's domain name link in the DNS name field.
    •	In a new browser window or tab, paste the domain name link in the address bar and press Enter.
    •	Observe which website you are directed to — Site 1 or Site 2 — since the Performance routing method will direct traffic to the site with the lowest latency time, which typically means the site closest to your physical location.
    
**Switch Routing Method to Priority to Switch Site Redirection and Observe the Results**

    •	Back in the Traffic Manager profile page, in the navigation menu on the left, under Settings, click Configuration.
    •	From the Routing method drop-down, select Priority.
    •	From the menu at the top, click Save.
    •	In the navigation menu on the left, click Overview.
    •	Observe that the site1-endpoint and site2-endpoint endpoints now have a value assigned in the Priority field. The lower the number, the higher the priority.
    •	Take note of which endpoint has the higher priority (i.e., a Priority value of 1).
    •	Navigate back to the browser window or tab where you accessed the Traffic Manager profile's domain name link, and refresh the page.
    •	Note: It can take some time for the Traffic Manager profile to update, so you may need to wait a few minutes and/or refresh the page numerous times for there to be any change to which site you are connected to.
    •	Observe which website you are directed to — Site 1 or Site 2 — and confirm it is the site with the higher priority, since the Priority routing method will direct traffic to the site with the highest priority.
    
**Simulate Failure and Observe Failover**

    •	Depending on which endpoint has the higher priority, navigate to the browser window/tab where its App Service web app resource is open.
    •	From the menu at the top, click Stop and, when prompted, click Yes.
    •	Once that resource has stopped, navigate back to the Traffic Manager profile page and, from the menu at the top, click Refresh.
    •	Observe that the Monitor status for the higher priority endpoint has changed to Stopped.
    •	Navigate back to the browser window or tab where you accessed the Traffic Manager profile's domain name link, and refresh the page.
    •	Note: It can take some time for the "failure" to take place and traffic to be routed to the failover site, so you may need to wait a few minutes and/or refresh the page numerous times for there to be any change to which site you are connected to.
    •	Observe which website you are directed to — Site 1 or Site 2 — and confirm it is the site with the lower priority, since traffic should be redirected to it because it is still up and running and acting as the failover.



