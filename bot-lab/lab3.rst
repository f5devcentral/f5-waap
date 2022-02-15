Lab 3: Protecting F5 Airlines using F5 Distributed Cloud Bot Protect 
====================================================================

In this lab we will configure F5 XC Bot Protect to protect the F5 Airlines web application backend (https://airline-backend.f5se.com)

There are two phases

1. Getting the traffic flowing via F5 XC 
2. Configuration of the F5 XC Bot Protect capability to protect the endpoints.

Note: There are two layers of bot protection available in F5 XC:

 - Basic signature based bot protection - configured as part of the App Firewall object.

 .. image:: ../_static/botprotect1.png


 - Advanced Bot Protection - configured as part of the Load Balancer object which includes sophisticated signal collection / capabilities for dealing with advanced/targeted adversaries\
   
 .. image:: ../_static/botprotect2.png


For the puprose of today's lab we will be configuring Advanced Bot Protection.


Lab 3 - Part 1 - Running a credential stuffing attack against F5 airlines
==========================================================================


As a dependancy for configuring bot protection for the F5 airlines web presence we must first configure F5 Distributed cloud to be able to provide services for F5 airlines. This requires the following configuration:


 - You have logged into F5 XC console (lab1)
 - An origin pool - Origin pools specify where the origin resources to be protected are located. In this case we'll be protecting https://airline-backend.f5se.com/
 - A load balancer - F5 distributed cloud bot protection capabilities are applied as part of the load balancer profile.


Lab 3 - Part 1 - Exercise 1: Get traffic flowing: Creating an origin pool
-------------------------------------------------------------------------

 -  Log into F5 Distributed Cloud Console (as per lab 1)

#. Start in F5 Distributed Cloud Console and find the "Web App & API Protection" service from the services drop down.

 .. image::  ../_static/lbsetup1.png

#. Navigate to Manage -> Load Balancers -> Origin Pools

 .. image::  ../_static/lbsetup2.png

#. Click "Add Origin Pool"

 .. image::  ../_static/lbsetup3.png

#. Name the pool "airline-origin"

#. Under "Orgin Servers" click "Add Item"

#. Select "Public DNS Name of Origin Serer" - in this case we will be communicating to the origin based on it's DNS name over the internet. 

#. Enter "airline-backend.f5se.com" into the DNS name

#. Click "Add Item" to save the origin server defintiion.

 .. image::  ../_static/lbsetup4.png

#. Under TLS configuration - Select "TLS" - as communication between F5 distributed cloud and the origin will be secured using TLS.

 .. image::  ../_static/lbsetup5.png

#. Click "Save and Exit" to save the origin pool 

 .. image::  ../_static/lbsetup6.png


Lab 3 - Part 1 - Exercise 2: Getting traffic flowing: Creating a Load Balancer
------------------------------------------------------------------------------

#. Start in F5 Distributed Cloud Console and find the "Web App & API Protection" service from the services drop down.

#. Navigate to Mange -> Load Balancers -> HTTP Load Balancers 

 .. image::  ../_static/lbsetup7.png

#. Click "Add HTTP load balancer"

 .. image::  ../_static/lbsetup8.png

#. Name your load balancer "airline"

#. Input "airline.f5demo.com" as the domain
 - Note: If you have a DNS sub-domain deligated to F5 Distributed Cloud - you can use this domain. For the purposes of this lab we will access the load balancer using its CNAME.

 .. image::  ../_static/lbsetup9.png

#. Under "Default Origin Servers" select "Add Item"

 .. image::  ../_static/lbsetup10.png

#. Select the "airline-origin" origin pool object we recently created from the drop down list

#. Click "Add Item" to save the origin pool association

 .. image::  ../_static/lbsetup11.png

#. Click "Save and Exit" to save and create the load balancer object.

#. You will now be able to see the "airline" load balancer in the HTTP load balancers list



Lab 3 - Part 1 - Exercise 3: Getting traffic flowing: Check that you can reach the airline site via the F5 distributed cloud
----------------------------------------------------------------------------------------------------------------------------

#. Start in F5 Distributed Cloud Console and find the "Web App & API Protection" service from the services drop down.

#. Navigate to Mange -> Load Balancers -> HTTP Load Balancers 

#. Identify the "airline" HTTP load balancer - Under the DNS info column you will see a CNAME reference which represents the DNS name for the F5 distributed cloud service - Click on the copy value button ()

 .. image::  ../_static/lbsetup12.png

#. Paste the copied CNAME into a web browser. The F5 airlines site should load. These application flows are being processed via the F5 distributed cloud.

 .. image::  ../_static/lbsetup13.png

 #. This traffic has been handled by the F5 distributed cloud where application services such as WAF, API Protection and Bot Protection can now be applied.


Lab 3 - Part 2 - Setting up F5 Distributed Cloud Bot Protect
============================================================

Now that we've got traffic for our application flowing via F5 Distributed Cloud - we can now add the F5 XC Bot Service to our load balancer configuration

- Note: F5 DX provides both basic, signature based bot protection as part of the App Firewall configuration object and advanced bot protection as part of the load balancer configuration. For this lab we will be configuring advanced bot protection - which is a sub object of the load balancer configuration.


Lab 3 - Part 2 - Exercise 1: Get traffic flowing: Seting up F5 XC Bot Protect
-----------------------------------------------------------------------------

#. Start in F5 Distributed Cloud Console and find the "Web App & API Protection" service from the services drop down.

 .. image:: ../_static/lbsetup1.png

#. Navigate to Mange -> Load Balancers -> HTTP Load Balancers

 .. image:: ../_static/lbsetup7.png

#. Identify the "airline" HTTP load balancer - From the actions column click on the dropdown and selet "Manage Configuration"

#. Click "Edit Configuration" to open the configuration editor.

 .. image:: ../_static/botsetup1.png

#. F5 XC Bot Protect is configured under "Security Configuration"

 .. image:: ../_static/botsetup2.png

#. From the "Bot Defense Config" section select "Specify Bot Defense Configuration" from the dropdown.

 .. image:: ../_static/botsetup3.png

#. From the "Bot Defense Regional Endpoint" dropdown select the region that is closest to where the origin resources to be protected are hosted - In this case the origin is hosted in the US - So selet "US"

#. Select "Configure" for "Bot Defense Policy" - this is where we can configure the location that javascript is injected from and the sensetive application flow paths to be protected.

 .. image:: ../_static/botsetup4.png

#. Under "App Endpoint Type" - Click Configure

 .. image:: ../_static/botsetup5.png

#. Click "Add Item" to add an endpoint to be protected 

 .. image:: ../_static/botsetup6.png

#. Name the application endpoint "login"

#. Select "POST" as the HTTP method
 - Note: What we are configuring is what endpoints should be sent to the F5 Distributed Cloud Bot Protect service backend - Requests need to be sent to the backend by the browser along with the telemetary collected by the javascript executing in the client. As a result - directing GET/PUT/ANY endpoints to the backend will fail. This will be resolved in a forthcoming release.

 .. image:: ../_static/botsetup7.png
 
 #. - In this case we want to protect the login form (/user/login) - enter this into the prefix match
 #. Additionally we want this configuration to block requests that are identified as bots - Select "Block" from the bot mitigation action dropdown.
 #. Click Add Item to add this path to be protected.

 .. image:: ../_static/botsetup8.png

#. Click Apply to save the protected endpoint definitions

 .. image:: ../_static/botsetup9.png

#. Review the Javascript insertion settings - This will configure the javascript path name and the relevant place within the DOM to insert the F5 XC Bot Protect javascript. 
#. Click Apply to apply the F5 XC Bot Protect settings

 .. image:: ../_static/botsetup10.png

#. Click "Save and Exit" to save the LB configuration with the bot protect capability enabled.


Next: |bot-lab4| 

.. |bot-lab4| raw:: html

            <a href="https://github.com/f5devcentral/f5-waap/tree/main/bot-lab/lab4.rst" target="_blank">Lab 4: Attempt to use automation tools againt the protected website</a>
