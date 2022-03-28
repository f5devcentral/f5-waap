F5 Distributed Cloud Client-Side Defense (CSD) Lab 101
======================================================

`Last updated: 2022-03-23 6:00 PM CET`

Prerequisites
-------------


1. An account for F5 Distributed Cloud and a tenant with Client-Side Defense add-on capability provisioned.

2. An application which is accessible via the internet and where you can add the JavaScript the website. Alternativeley you can find instructions how to inject the JavaScript for testing purposes with the Chrome browser.
  
For *F5 SEs* the JavaScript was already added to the demo application and you can find the detais and login instructions for the f5-sales-demo tenant further down in the lab guide. 

You can sign up for a free account for the F5 Distributed Cloud in case you don't have an account yet by following the `sign up description <https://github.com/f5devcentral/f5-waap/blob/main/step-1-signup-deploy/voltConsole.rst>`_ or just go directly to the `sign up page <https://console.ves.volterra.io/signup/usage_plan>`_


What we'll learn
----------------

During this hands-on lab you will learn about the following: 

- High level introduction in the use case of Client Side Defense (CSD)
- Log into the F5 XC Console
- Configure CSD, logging and add the JavaScript to the web server
- Check if the telemetry data are sent to F5
- Using the Client Side Defense dashboard to mitigate suspicious domains
- Show that requests to suspicious domains are blocked

Lab Environment
---------------

During this lab you can use your own F5 Distributed Cloud account and your own application (origin server) that you are going to protect with CSD. Alternatively you can also use the F5 sales-demo application where we already added the requird JavaScript tag for CSD https://shop.sales-demo.f5demos.com.

|

Please contact your F5 Sales Engineer/Account Manager if you need more information and please send any feedback for this lab to a.vistola@f5.com

|

F5 Distributed Cloud Client Side Defense: Prevent Skimming and Formjacking
--------------------------------------------------------------------------
Like credit card skimming in the physical world, cybercriminals have developed attacks to take ownership of legitimate websites and install digital skimming to steal credit card numbers, social security numbers, national identity numbers, names, addresses, login credentials, and other personally identifiable information.

Chief information security officers (CISOs) face a client-side security gap that puts their customers’ privacy and financial well-being at risk. With Magecart-like criminal attacks against websites causing massive breaches, government fines, and loss of customer confidence, the challenge of keeping customers safe online needs urgent attention.

Client-Side Monitoring, Detection, and Mitigation
-------------------------------------------------
Distributed Cloud Client-Side Defense has two core components that establish its efficacy:

JavaScript that captures signals and a machine learning analysis service that processes those signals.

.. image:: ../_static/csd-diagram.png

|

Next: |signup|

.. |signup| raw:: html

            <a href="https://github.com/f5devcentral/f5-waap/blob/main/lab1.rst" target="_blank">Lab 1: Base Configuration of CSD</a>


