Using the Client Side Defense Dashboard
=======================================

Lab 2: Mitigate suspicious or allow unsuspicious domains
-------------------------------------------------------------

Login to F5 Distributed Cloud using your own account or f5-sales-demo using the credentials for the read only account from the `f5-sales-demo tenant <https://teams.microsoft.com/l/message/19:45ba7ac2ebb540ecb3b44929aebd7e99@thread.tacv2/1645109960193?tenantId=dd3dfd2f-6a3b-40d1-9be0-bf8327d81c50&groupId=2dc42443-8b46-4694-aa58-defbd3dc8a4b&parentMessageId=1645109960193&teamName=SME-Volterra&channelName=Sales%20Demo%20Tenant%20Ops&createdTime=1645109960193>`_ and go to the Client-Side Defense dashboard.
I recommend to login to the f5-sales-demo account for the next steps of this lab or generate some artificially injections with suspicious domains which is explained in **appendix A** before you start this lab.

.. image:: ../_static/csd-dashboard.png

|

The CSD Dashboard displays the following tabs that you use for displaying data, and for deciding whether to mitigate or allow a suspicious domain:

.. image:: ../_static/csd-tabs.png

*Suspicious Domains:* When a web page with CSD protection is loaded on the end-user’s browser, scripts running on that web page interact with other domains. The Suspicious Domains list displays a list of the domains that those scripts interact with and which CSD detected to be potentially malicious.

*Mitigate List:* Displays a list of domains that the user has assigned for mitigation. When a domain is assigned for mitigation, CSD blocks that domain and it cannot be accessed by any script running on the end-user's browser when accessing a CSD protected web page.
    
*Allow List:* Displays a list of domains that the user has decided do not need mitigation and can be allowed free access.
    
*All Domains:* When a web page with CSD protection is loaded, scripts running on that web page interact with other domains. The All Domains list displays a list of the domains that those scripts interact with.

|

1. Viewing suspicious domains
 
 Click on suspicious domains to display the list of the potentially malicious domains. "Select Page" on the right allows to filter.

 .. image:: ../_static/csd-suspicious-domains.png

 .. note:: You see suspicious domains when you login to the f5-sales-demo tenant but you probably won't see them when you use your own environment with no live traffic. Please see the **appendix A** to generate artificially suspicious domain entries.
  
|

2. Adding a domain to the Mitigate List or Allow List
   
 Go to the row of the relevant domain and select the appropriate action on the right by clicking on the three dots. Our example shows how to add the domain jqwereid.online to the Mitigate List. It goes first in the state Added to Mitigated List (green) and change after some time to status Mitigated (blue). 
 Alternatively, you can add domains manually to the Mitigate List or Allow List by going to the Mitigate List or Allow List at the top and, click on Add domain and enter the domain name.

  .. note:: The monitor user for the f5-sales-com account has read only rights and therefore you can't save your modifications and you will see a 403 forbidden but e.g. the domain fountm-online is already set to mitigated to block requests to this domain which is needed for the next chapter.
 
 .. image:: ../_static/csd-mitigate.png

|

 Status - Added to Mitigated List

 .. image:: ../_static/csd-mitigate-added.png

|

 Status - Mitigated

 .. image:: ../_static/csd-mitigated.png

|

3. Show that requests to the mitigated domains are blocked
 
 Open a browser, go to https://shop.sales-demo.f5demos.com/ and start the browser's DevTools.

 Have the network tab and console tab open as shown below and copy & paste the following code into the console::

   var s = document.createElement('script')
   s.src = "https://fountm.online/"
   document.body.appendChild(s)

 Press enter and you should see the message  *GET https://fountm.online/ net::ERR_CONNECTION_REFUSED* and the request shows up in the network tab with the *status failed*

 .. image:: ../_static/csd-block-susp-domain.png

4. Show that other requests from the browser (script) are still allowed

 Copy & paste the following code into the console::

   var s = document.createElement('script')
   s.src = "https://www.google.com/"
   document.body.appendChild(s)

 Press enter and you should see that the request is successful and shows up in the network tab with the *status 200*

 .. image:: ../_static/csd-block-susp-allow-other.png

|

5. Appendix - Generate artificially suspicious domains
