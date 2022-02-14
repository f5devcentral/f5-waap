Lab 3 - Part 2 - Setting up F5 Distributed Cloud Bot Protect
============================================================

Now that we've got traffic for our application flowing via F5 Distributed Cloud - we can now add the F5 XC Bot Service to our load balancer configuration

- Note: F5 DX provides both basic, signature based bot protection as part of the App Firewall configuration object and advanced bot protection as part of the load balancer configuration. For this lab we will be configuring advanced bot protection - which is a sub object of the load balancer configuration.


Lab 3 - Part 2 - Exercise 1: Get traffic flowing: Seting up F5 XC Bot Protect
-----------------------------------------------------------------------------

#. Start in F5 Distributed Cloud Console and find the "Web App & API Protection" service from the services drop down.

 .. image:: /_images/lbsetup1.png

#. Navigate to Mange -> Load Balancers -> HTTP Load Balancers

 .. image:: /_images/lbsetup7.png

#. Identify the "airline" HTTP load balancer - From the actions column click on the dropdown and selet "Manage Configuration"

#. Click "Edit Configuration" to open the configuration editor.

 .. image:: /_images/botsetup1.png

#. F5 XC Bot Protect is configured under "Security Configuration"

 .. image:: /_images/botsetup2.png

#. From the "Bot Defense Config" section select "Specify Bot Defense Configuration" from the dropdown.

 .. image:: /_images/botsetup3.png

#. From the "Bot Defense Regional Endpoint" dropdown select the region that is closest to where the origin resources to be protected are hosted - In this case the origin is hosted in the US - So selet "US"

#. Select "Configure" for "Bot Defense Policy" - this is where we can configure the location that javascript is injected from and the sensetive application flow paths to be protected.

 .. image:: /_images/botsetup4.png

#. Under "App Endpoint Type" - Click Configure

 .. image:: /_images/botsetup5.png

#. Click "Add Item" to add an endpoint to be protected 

 .. image:: /_images/botsetup6.png

#. Name the application endpoint "login"

#. Select "POST" as the HTTP method
 - Note: What we are configuring is what endpoints should be sent to the F5 Distributed Cloud Bot Protect service backend - Requests need to be sent to the backend by the browser along with the telemetary collected by the javascript executing in the client. As a result - directing GET/PUT/ANY endpoints to the backend will fail. This will be resolved in a forthcoming release.

 .. image:: /_images/botsetup7.png
 
 #. - In this case we want to protect the login form (/user/login) - enter this into the prefix match
 #. Additionally we want this configuration to block requests that are identified as bots - Select "Block" from the bot mitigation action dropdown.
 #. Click Add Item to add this path to be protected.

 .. image:: /_images/botsetup8.png

#. Click Apply to save the protected endpoint definitions

 .. image:: /_images/botsetup9.png

#. Review the Javascript insertion settings - This will configure the javascript path name and the relevant place within the DOM to insert the F5 XC Bot Protect javascript. 
#. Click Apply to apply the F5 XC Bot Protect settings

 .. image:: /_images/botsetup10.png

#. Click "Save and Exit" to save the LB configuration with the bot protect capability enabled.