Using the Client Side Defense Dashboard
=======================================

Lab 2: Mitigate suspicious or allow unsuspicious domains
--------------------------------------------------------

Login to F5 Distributed Cloud using your own account or optional for *F5 SEs*, login into the f5-sales-demo tenant using the credentials for the read only account from the `f5-sales-demo tenant <https://teams.microsoft.com/l/message/19:45ba7ac2ebb540ecb3b44929aebd7e99@thread.tacv2/1645109960193?tenantId=dd3dfd2f-6a3b-40d1-9be0-bf8327d81c50&groupId=2dc42443-8b46-4694-aa58-defbd3dc8a4b&parentMessageId=1645109960193&teamName=SME-Volterra&channelName=Sales%20Demo%20Tenant%20Ops&createdTime=1645109960193>`_ and go to the Client-Side Defense dashboard.

|

.. note:: I've generated some artificially injections with suspicious domains for the f5-sales-demo tenant to make demos easier. If you use your own website, you can generate some artificially injections with suspicious domains as explained in **Appendix A** at the end of this document, before you continue this lab.

|

Once you logged in, click on *Client-Side Defense*.

 .. image:: ../_static/csd-dashboard.png

|

The CSD Dashboard displays the following tabs that you use for displaying data, and for deciding whether to mitigate or allow a suspicious domain.

 .. image:: ../_static/csd-tabs.png

*Suspicious Domains:* When a web page with CSD protection is loaded on the end-user’s browser, scripts running on that web page interact with other domains. The Suspicious Domains list displays a list of the domains that those scripts interact with and which CSD detected to be potentially malicious.

*Mitigate List:* Displays a list of domains that the user has assigned for mitigation. When a domain is assigned for mitigation, CSD blocks that domain and it cannot be accessed by any script running on the end-user's browser when accessing a CSD protected web page.
    
*Allow List:* Displays a list of domains that the user has decided do not need mitigation and can be allowed free access.
    
*All Domains:* When a web page with CSD protection is loaded, scripts running on that web page interact with other domains. The All Domains list displays a list of the domains that those scripts interact with.

|

1. Viewing suspicious domains
 
 Click on suspicious domains to display the list of the potentially malicious domains. "Select Page" on the right allows to filter.

 .. image:: ../_static/csd-suspicious-domains.png

 .. note:: You will see suspicious domains when you login to the *f5-sales-demo* tenant but you probably won't see them when you use your own website with no live traffic. Please see the **Appendix A** at the end of this document to generate artificially suspicious domain entries.
  
|

2. Adding a domain to the Mitigate List or Allow List
   
 Go to the row of the relevant domain and select the appropriate action on the right by clicking on the *three dots*. Our example shows how to add the domain jqwereid.online to the Mitigate List. It goes first in the state Added to Mitigated List (green) and change after some time to status Mitigated (blue). 
 Alternatively, you can add domains manually to the Mitigate List or Allow List by going to the Mitigate List or Allow List at the top and, click on *Add domain* and enter the domain name.

 .. note:: The monitor user for the f5-sales-com account has read only rights and therefore you can't save your modifications and you will see a 403 forbidden but e.g. the domain fountm-online is already set to mitigated to block requests to this domain which is needed for the next chapter.
 
 .. image:: ../_static/csd-mitigate.png

|

 Status - Added to Mitigated List

 .. image:: ../_static/csd-mitigate-added.png

|

 Status - Mitigated

 .. image:: ../_static/csd-mitigated.png

|

3. Show that requests from scripts to the mitigated domains are blocked
 
 Open a browser, go to https://shop.sales-demo.f5demos.com/ and start the browser's DevTools.

 Have the network tab and console tab open as shown below and copy & paste the following code into the console::

   var s = document.createElement('script')
   s.src = "https://fountm.online/"
   document.body.appendChild(s)

 Press enter and you should see a message like in the screenshot below and no request in the network tab.

 .. image:: ../_static/csd-block-susp-domain.png

|

4. Show that requests from scripts to benign domains are allowed

 Copy & paste the following code into the console::

   var s = document.createElement('script')
   s.src = "https://www.google.com/"
   document.body.appendChild(s)

 Press enter and you should see that the request is successful and shows up in the network tab with the *status 200*

 .. image:: ../_static/csd-block-susp-allow-other.png

|

Appendix A - Artificially generate suspicious domains
=====================================================

1. Navigate to a website like https://db.aa419.org/fakebankslist.php to look for fake sites.

 .. note:: **DISCLAIMER:** artists against 419 ("aa419") identifies fraudulent websites and makes this data available as a public service. We discourage any form of communication with these websites. If you chose to communicate with them you do so at your own risk.

2. Use any of the following methods to add the code below to the html code of your testing website.

 - Local overrides in Chrome Developer Tools as described in **Appendix B** at the end of this document.
 - Local proxy like Charles proxy
 - Or just add the code to your testing web site but don't foget to remove it after the test.

.. note:: For demoing purposes, we have added already a similar code as shown below to the sales demo app https://shop.sales-demo.f5demos.com/. You can verify it by viewing the source code of the web page.

 You can use the code as shown below with the fake domains or replace the fake domains with the ones you want to use for the test::
  </script><script>(function(){var s=document.createElement("script");var domains=["ganalitis.com","ganalitics.com","gstatcs.com","webfaset.com","fountm.online","pixupjqes.tech","jqwereid.online"];for (var i=0; i < domains.length; ++i){s.src="https://" + domains[i];}})();</script>

 .. note:: The browser doesn't send a request to the specified domains by adding or injecting the code as shown above.

|

 Example what you should see when you view the source code of the page.

 .. image:: ../_static/csd-view-source-color.png

|


Appendix B - Injection using local Overrides in Chrome
======================================================

.. note:: This injection method can be used to inject code locally on your browser. The following example shows you how to inject code to artificially generate suspicious domains but of course you can also inject the CSD JavaScript from your tenant in addition, to test for instance a website you don't own. **The DevTools need to be kept open for the test.**

Set up local Overrides in Chrome DevTools
-----------------------------------------

#. Open Chrome DevTools.
#. Click on the *Sources* tab.
#. Click on the *Overrides* tab.
#. Click on *Select folder for overrides*.

 .. image:: ../_static/csd-select-folder-overrides.png

|

5. Select which directory you want to save your changes to.
#. At the top of your window, click **Allow** to give DevTools read and write access to this directory.
#. Make sure *"Enable Local Overrides"* is checked.

 .. image:: ../_static/csd-select-folder-overrides-selected.png

|

8. Click on the *Network tab*.
#. Open the page, in this example https://arcadia.emea.f5se.com/
#. Select the page or a file like index.html that you want to override. In our example "arcadia.emea.f5se.com". Just refresh if you don’t see it in the network tab.

 .. image:: ../_static/csd-select-page.png

|

11. Right click on the code on the right side and select "Save for overrides".

 .. image:: ../_static/csd-save-for-overrides.png

|

#. Make your code changes on the right side.
 
 .. image:: ../_static/csd-add-injection-code.png

|

#. **And make sure you save your changes afterwards e.g. with Ctrl+S or Command+S!**

.. note:: You won't see the overwritten code when you click on *view source code* in the page. If you want to check if the overwrite works, you can e.g. modifiy a title or a text on the page to see the changes on the screen.
