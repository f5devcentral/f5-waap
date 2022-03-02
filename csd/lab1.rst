Lab 1: Login and Enable CSD
######################################

Login
=====

Navigate to https://www.f5.com/cloud, select login at the top right and finally select your account type to login.

    .. note:: You can sign up for a free account for the F5 Distributed Cloud in case you don't have an account yet by following the sign up description https://github.com/f5devcentral/f5-waap/blob/main/step-1-signup-deploy/voltConsole.rst or just go directly to the sign up page https://console.ves.volterra.io/signup/usage_plan.

.. image:: ../_static/csd-login.png

Create Public Origin Pool
~~~~~~~~~~~~~~~~~~~~~~~~~
We will first create an Origin Pool that refers to the "Public E





Lab 2 - Part 1 : Logging into the Unified Demo Framework
========================================================

In this exercise we will be suing the "Automation" unified demo framework blueprint - This blueprint provides a Windows image with many tools and frameworks often used by advesaries to exploit attacks leveraging automation.

Tools include:
 - PyCharm with a basic Selenium webdriver configuration.
 - Sentry MBA
 - GatherProxy
 - webscraper.io
 - Selenium IDE
 - Puppeteer w/reCAPTCHA


Lab 2 - Exercise 1: Deploy, start and log into the UDF blueprint
----------------------------------------------------------------

#. Login to UDF https://udf.f5.com using your employee or partner credentials (Speak to your account manager or F5 contact for access)

 .. image:: ../_static/udf1.png

#. Navigate to the blueprint and find the "Athena Attacker blueprint" (https://udf.f5.com/b/c069bba3-17fd-4466-843e-f9a90c5255a4#documentation)

 .. image:: ../_static/udf2.png

#. Click Deploy

#. Once the UDF blueprint has deployed - Start the deployment

 .. image:: ../_static/udf3.png

#. Log into the "Launchpad" system using deployment using RDP - The credentials are available in the udf blueprint documentation

 .. image:: ../_static/udf4.png


Lab 2 - Part 2  : Running a credential stuffing attack against F5 airlines
==========================================================================

Lab 2 - Part 2: Exercise 1: Credential Stuffing with OpenBullet 2