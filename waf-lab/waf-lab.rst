.. _waf_lab:

Secure the F5XC Microservices Demo App
######################################

Create Origin Pools
===================

Before we create an HTTP load balancer to expose our app on the internet, 
we'll define "Origin Pools" for our application's services.

This initial Origin Pool will use the Public DNS record of our target webserver 
to locate the IP address of the Origin Pool members.  This is an example of using 
the Public Internet to route traffic to our services.

    .. note:: Deployed F5XC Microservices Demo App exposed a frontend microservice using specified domain delegated to F5 Distributed Cloud Platform. The app can be protected by attaching a WAF object to an existing LB however in the interest of this lab we will execute through the process of creating an LB and protecting it with F5 Distributed Cloud WAF. F5 Distributed Cloud WAF can also protect an existing customer application that is located for instance on-premises, private or public Cloud whith similar configuration steps. 

Create Public Origin Pool
~~~~~~~~~~~~~~~~~~~~~~~~~
We will first create an Origin Pool that refers to the "Public Endpoint" site in our tenant.

#. Start in F5DC Console and switch to the "Web App & API Protection" context. [You should already be here from previous step]

    |app-context|

#. Next select namespace created in "Sign-up for F5 WAAP Service" step

   .. image:: ../_static/app-ns.png 

#. Navigate the menu to go to ``Manage`` -> ``Load Balancers`` -> ``Origin Pools``. Click on ``Add Origin Pool``.

#. Enter the following variables:

    ================================= =====
    Variable                          Value
    ================================= =====
    Name                              public
    ================================= =====

#. Click on "Add Item" under the section "Origin Servers"

   Enter the following variables: 

    ================================= =====
    Variable                          Value
    ================================= =====
    Select Type of Origin Server      Public DNS Name of Origin Server [default]
    DNS Name                          <subdomain>.f5demos.com
    ================================= =====
    
    |op-pool-basic|

    Click on "Add Item" to return to the previous screen.

#. Below the "Origin Servers" section fill in the Port information

    ================================= =====
    Variable                          Value
    ================================= =====
    Port                              443
    ================================= =====


#. Under the *List of Health Check(s)* section, click the *Add item* button.

#. Click the *Health Check object* dropdown list. Click the *Create new healthcheck* button.

#. Enter the following variables:

    ========= =====
    Variable  Value
    ========= =====
    name      http
    ========= =====

#. Click the *Configure* button under "HTTP Health Check" and enter the following variables ("/" is the default):

    ========= =====
    Variable  Value
    ========= =====
    path      /
    ========= =====

#. Click *Apply* to exit the "Health Check HTTP Parameters" dialogue.
#. Under ``TLS Configuration`` expand the dropdown list and select "TLS". Leave other parameters default

    |tls|


#. Click *Continue* to return to the "Origin Pool" configuration.
#. Click the *Save and Exit* button to create the Origin Pool.

.. |app-context| image:: ../_static/app-context.png
.. |origin_pools_menu| image:: ../_static/origin_pools_menu.png
.. |origin_pools_add| image:: ../_static/origin_pools_add.png
.. |origin_pools_config| image:: ../_static/origin_pools_config.png
.. |origin_pools_config_api| image:: ../_static/origin_pools_config_api.png
.. |origin_pools_config_mongodb| image:: ../_static/origin_pools_config_mongodb.png
.. |origin_pools_show_child_objects| image:: ../_static/origin_pools_show_child_objects.png
.. |origin_pools_show_child_objects_status| image:: ../_static/origin_pools_show_child_objects_status.png
.. |http_lb_origin_pool_health_check| image:: ../_static/http_lb_origin_pool_health_check.png
.. |http_lb_origin_pool_health_check2| image:: ../_static/http_lb_origin_pool_health_check2.png

.. |op-add-pool| image:: ../_static/op-add-pool.png
.. |op-api-pool| image:: ../_static/op-api-pool.png
.. |op-pool-basic| image:: ../_static/op-pool-basic.png
.. |op-spa-check| image:: ../_static/op-spa-check.png
.. |op-tshoot| image:: ../_static/op-tshoot.png
.. |lb-basic| image:: ../_static/lb-basic.png
.. |tls| image:: ../_static/tls.png


Create WAF Policy
=================

F5 Distributed Cloud Platform WAF shares the same WAF engine that is used by F5 BIG-IP WAF and F5 NGINX App Protect.

The F5 Distributed Cloud Platform WAF engine provides preset categories of rules to protect your web 
applications, provides the ability to run in a monitor or blocking mode, prevent 
false positives by excluding individual rules, IP addresses, or web application paths

In the next exercise you will configure a basic WAF policy 

Create WAF Policy
~~~~~~~~~~~~~~~~~~

We will create a blocking WAF policy.

#. Start in F5DC Console and switch to the "Web App & API Protection" context. 

   It can be access either from the main Home page or via the "Select Service" menu on a Page 

    |app-context|

#. Navigate the menu to go to ``Manage`` -> ``App Firewall``. Click on *Add App Firewall*.


#. Enter the following variables:

    ================================= ============================================
    Variable                          Value
    ================================= ============================================
    Name                              blocking-app-firewall
    Enforcement Mode                  Blocking
    ================================= ============================================

    In this mode we have change the policy to block attacks that are included in 
    the default policy.  Later we will look at how we can customize these settings.

    .. image:: ../_static/blocking-app-firewall-policy.png

#. Leave the *Detection Settings* as Default and Click the *Save and Exit* button to create the policy



Creating HTTP Load Balancer on F5 Distributed Cloud Platform Regional Edge
==========================================================================

In this exercise we will be creating a "Global VIP" that will exist on the F5 Distributed Cloud Platform Global Network.

It will protect a public resource that points to the F5XC Microservices Demo App frontend origin.



HTTP Load Balancer Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Start in F5DC Console and switch to the "Web App & API Protection" context. [You should already be here from previous lab]

#. Navigate the menu to go to ``Manage`` -> ``Load Balancers`` -> ``HTTP Load Balancers`` and click on "Add HTTP Load Balancer".

#. Enter the following variables:

    ================================= =====
    Variable                          Value
    ================================= =====
    Name                              global
    Domains                           <yourName>.f5demos.com
    Select type of Load Balancer      HTTP
    Automatically Manage DNS Records  No/Unchecked 
    ================================= =====

    |lb-basic|

Configure Default Origin Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
We'll next configure the "Default Origin Servers". 
    
#. Click on the *Add Items* link under the *Default Origin Servers* section.

#. The "Select Origin Pool Method" will be set to "Origin Pool". Under the "Origin Pool" dropdown menu select the "public" pool you created earlier.

   .. image:: /_static/lb-pool-public.png
 
#. Click the *Add Item* button to exit the "Origin Pools" dialogue.

#. Notice that in the "VIP Configuration" section *Advertise On Internet* has been selected by default.

Configure WAF Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Under the *Security Configuration* section

#. Leave the Service Policies as "Apply Namespace Service Policies" (default) and the Bot Defense Config will be covered in a seperate lab.

#. Enter the following variables:

    ============================================= =====================
    Variable                                      Value
    ============================================= =====================
    Select Web Application Firewall (WAF) Config  App Firewall
    App Firewall                                  blocking-app-firewall
    ============================================= =====================

    .. image:: ../_static/lb-security-configuration.png


#. Click "*Save and Exit* to create the HTTP Load Balancer".

Once the HTTP Load Balancer has been deployed, you should now be able to go to the "ves.io" CNAME that has been generated. 

    .. note::  A CNAME record for the subdomain of choice be created in DNS provider to reach the LB using subdomain URL. For the purpose of this lab this step is optional.

Verify Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The F5XC Microservices Demo App should look like the following:

.. image:: ../_static/screenshot-global-vip-public.png
  :width: 70%

In this topology we are sending traffic to an AnyCast IP that is hosted in F5 Distributed Cloud Platform's Regional Edge.

We then connect to the Origin via it's Public DNS name (exposed by the LB in different namespace)

Try adding the following to the URL "/?cat%20/etc/passwd".

You should see a block page.

.. image:: ../_static/screenshot-global-vip-public-cat-etc-passwd.png
  :width: 70%

Performance and Security 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Start in F5DC Console and switch to the "Web App & API Protection" context. [You should already be here from previous lab]

We can view details of successful requests and blocks by navigating to "Apps & APIs"

#. Click on ``Apps & APIs`` -> ``Security`` and click on your "global" Load Balancer (bottom right)

   .. image:: ../_static/security-overview.png
       :width: 70%

   You will see various chicklets showing "Top Attack Types", "Top Signatures Hit", "Security Events by Location" etc.

   .. image:: ../_static/screenshot-global-vip-security-dashboard.png
       :width: 70%

#. Click on "Requests" in the upper page navigation

   You should be able to view logs for individual requests.

   .. image:: ../_static/screenshot-global-vip-public-requests.png
       :width: 70%

#. Click on "Security Events"
   You will be able to see details of the security events.

   .. image:: ../_static/screenshot-global-vip-public-security-events.png
       :width: 70%   

   Clicking on the arrow to the left of a security event will expand the details.

   .. image:: ../_static/screenshot-global-vip-public-security-events-details.png
       :width: 70%



Video Walkthrough 
~~~~~~~~~~~~~~~~~
Optional Videos you can watch if you get stuck

#. .. raw:: html
   
    <a href="https://player.vimeo.com/video/420386926?h=825a452739" target="_blank">Step One</a>

#. .. raw:: html

    <a href="https://player.vimeo.com/video/420389494?h=8fdd942550" target="_blank">Step Two</a>

#. .. raw:: html

    <a href="https://player.vimeo.com/video/420391402?h=f2fcc22c33" target="_blank">Step Three</a>


This completes the F5 XC WAF lab.