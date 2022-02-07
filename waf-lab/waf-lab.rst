Create Origin Pools
====================

Before we create an HTTP load balancer to expose our app on the internet, 
we'll define "Origin Pools" for our application's services.

This initial Origin Pool will use the Public DNS record of our target webserver 
to locate the IP address of the Origin Pool members.  This is an example of using 
the Public Internet to route traffic to our services.  In later examples we will 
look at routing traffic via VoltMesh to our services.

Exercise 1: Create Public Origin Pool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
We will first create an Origin Pool that refers to the "Public Endpoint" site in our lab environment.

#. Start in VoltConsole and switch to the "Web App & API Protection" context. [You should already be here from previous lab]

#. Navigate the menu to go to "Manage"->"Load Balancers"->"Origin Pools". Click on *Add Origin Pool*.

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
    DNS Name                          public.lab.f5demos.com
    ================================= =====
    
    |op-pool-basic|

    Click on "Add Item" to return to the previous screen.

#. Below the "Origin Servers" section fill in the Port information

    ================================= =====
    Variable                          Value
    ================================= =====
    Port                              80
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


Create WAF Policy
=================

Volterra WAF shares the same WAF engine that is used by F5 BIG-IP WAF and F5 NGINX App Protect.

The Volterra WAF engine provides preset categories of rules to protect your web 
applications, provides the ability to run in a monitor or blocking mode, prevent 
false positives by excluding individual rules, IP addresses, or web application paths

In the next exercise you will configure a basic WAF policy 

Exercise 1: Create WAF Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We will create a blocking WAF policy.

#. Start in VoltConsole and switch to the "Web App & API Protection" context. 

   It can be access either from the main Home page or via the "Select Service" menu on a Page 

    |app-context|

#. Navigate the menu to go to "Manage"->"App Firewall". Click on *Add App Firewall*.


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

#. Click the *Save and Exit* button to create the policy

Video Walkthrough 
~~~~~~~~~~~~~~~~~
Optional Video you can watch if you get stuck

Note that each of the videos will start at a specific timestamp.  

The entire video is 10 minutes total from start to finish.

.. raw:: html
   
   <iframe width="560" height="315" src="https://www.youtube.com/embed/s-BHH0Qayfc?start=41" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

.. |app-context| image:: ../_static/app-context.png
    :width: 75%

    

Creating HTTP Load Balancer on Volterra Regional Edge
=====================================================

In this exercise we will be creating a "Global VIP" that will exist on the Volterra Global Network.

It will protect a public resource that exists in the lab's AWS Lab Environment.

.. image:: ../_static/testdrive-volterra-waf-global-vip.png

Exercise 1: HTTP Load Balancer Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Start in VoltConsole and switch to the "Web App & API Protection" context. [You should already be here from previous lab]

#. Navigate the menu to go to "Manage"->"Load Balancers" -> "HTTP Load Balancers" and click on "Add HTTP Load Balancer".

#. Enter the following variables:

    ================================= =====
    Variable                          Value
    ================================= =====
    Name                              global
    Domains                           studentXXX.sales-public.f5demos.com
    Select type of Load Balancer      HTTP
    Automatically Manage DNS Records  Yes/Check 
    ================================= =====

    |lb-basic|

Exercise 2: Configure Default Origin Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
We'll next configure the "Default Origin Servers". 
    
#. Click on the *Add Items* link under the *Default Origin Servers* section.

#. The "Select Origin Pool Method" will be set to "Origin Pool". Under the "Origin Pool" dropdown menu select the "public" pool you created earlier.

   .. image:: /_static/lb-pool-public.png
 
#. Click the *Add Item* button to exit the "Origin Pools" dialogue.

#. Notice that in the "VIP Configuration" section *Advertise On Internet* has been selected by default.

Exercise 3: Configure WAF Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Under the *Security Configuration* section 

#. Enter the following variables:

    ============================================= =====================
    Variable                                      Value
    ============================================= =====================
    Select Web Application Firewall (WAF) Config  App Firewall
    App Firewall                                  blocking-app-firewall
    ============================================= =====================

#. Click "*Save and Exit* to create the HTTP Load Balancer.

Once the HTTP Load Balancer has been deployed, you should now be able to go to the DNS name that you entered 
previously in a web browser.  The FQDN we used in our example is http://studentXX.sales-public.f5demos.com.  
Your FQDN should follow the format of [unique name].[supplied domain name for your tenant].

.. note:: If you are having challenges connecting to the "f5demos.com" name you can also try connecting to the "ves.io" name.

Exercise 4: Verify Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The public demo app should look like the following:

.. image:: ../_static/screenshot-global-vip-public.png
  :width: 50%

In this topology we are sending traffic to an AnyCast IP that is hosted in Volterra's Regional Edge.

We then connect to the AWS resource via it's Public IP address.  

Try adding the following to the URL "/?cat%20/etc/passwd".

You should see a block page.

.. image:: ../_static/screenshot-global-vip-public-cat-etc-passwd.png

Exercise 5: Performance and Security 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Start in VoltConsole and switch to the "Web App & API Protection" context. [You should already be here from previous lab]

We can view details of successful requests and blocks by navigating to "Apps & APIs"

#. Click on "Apps & APIs"->"Performance" and click on your "global" Load Balancer (bottom right)

   .. image:: ../_static/performance-overview.png
       :width: 50%

   You will see a  health score of your application as well as end to end latency of the connection.

   .. image:: ../_static/screenshot-global-vip-performance-dashboard.png
       :width: 50%

#. Click on "Requests" in the upper page navigation

   You should be able to view logs for individual requests.

   .. image:: ../_static/screenshot-global-vip-public-requests.png
       :width: 50%

#. Click on "Apps & APIs"->"Security" and click on your "global" Load Balancer (bottom right)
#. Click on "Security Events"
   You will be able to see details of the security events.

   .. image:: ../_static/screenshot-global-vip-public-security-events.png

   Clicking on the arrow to the left of a security event will expand the details.

   .. image:: ../_static/screenshot-global-vip-public-security-events-details.png
       :width: 50%


Next we will demonstrate how we 
can securely connect to your private AWS resources via a VoltMesh node.

Video Walkthrough 
~~~~~~~~~~~~~~~~~
Optional Video you can watch if you get stuck

.. raw:: html
   
   <iframe width="560" height="315" src="https://www.youtube.com/embed/s-BHH0Qayfc?start=108" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

.. |app-context| image:: ../_static/app-context.png
.. |lb-basic| image:: ../_static/lb-basic.png
