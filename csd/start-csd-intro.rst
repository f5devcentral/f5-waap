F5 Distributed Cloud Client Side Defense 101
============================================

`Last updated: 2022-02-25 6:00 PM CET`

F5 Distributed Cloud Client Side Defense: Prevent Skimming and Formjacking
--------------------------------------------------------------------------
Like credit card skimming in the physical world, cybercriminals have developed attacks to take ownership of legitimate websites and install digital skimming to steal credit card numbers, social security numbers, national identity numbers, names, addresses, login credentials, and other personally identifiable information.

Chief information security officers (CISOs) face a client-side security gap that puts their customers’ privacy and financial well-being at risk. With Magecart-like criminal attacks against websites causing massive breaches, government fines, and loss of customer confidence, the challenge of keeping customers safe online needs urgent attention.

Client-Side Monitoring, Detection, and Mitigation
-------------------------------------------------
Distributed Cloud Client-Side Defense has two core components that establish its efficacy:

JavaScript that captures signals and a machine learning analysis service that processes those signals.

.. image:: ../_static/csd-diagram.png


What we'll learn
================


During this hands-on lab you will learn about the following: 

- How to log into the F5 XC Console
- Threat landscape and bad actor evolution
- Examples of exploitation of common automated threats (Carding, Credential Stuffing) against the F5 demo site (F5 airlines)
- How to configure F5XC's SaaS based platform for controlling advanced automated threats
- How F5 bot protect identifies and blocks automated threats
- How to gain visibility into the automated threats targeting a web application using the F5XC 

Lab Environment
---------------

During this lab you will be using the shared F5XC `f5-sales-public` tenant (the first lab exercise will 
cover how to access this environment). We will be setting up F5 F5XC Bot Protect in front of our airline demo site .. _https://airline-backend.f5se.common

Our Demo App - F5 Airlines
--------------------------

In this lab we will be protecting our demo site - F5 Airlines - You can explore the F5 airlines website by navigating to https://airline-backend.f5se.com

Like many online web channels, F5  airlines has many functions that a bad actor could exploit leveraging automation

- A **signup form** - an attacker could use automation to create bulk accounts - This is an example of OAT-19 Account Creation. 



- A **login form** - an attacker could use automation to test a large number of credentials using brute force - this is an example of OAT-007 - Credential Cracking - or from a credential leak - This is an example of OAT-008 - Credential Stuffing
- A **credit card payment gateway** - an attacker could use automation to test a large number of stolen credit cards - an example of OAT-010 Card Cracking
- A **frequent flyer gift card system** - an attacker could use automation to brute force gift card IDs and PINs - an example of OAT-002 Token Cracking
- A **flight booking interface** - an attacker could use automation to block/hold all the seats on a flight - an example of OAT-021 Denial of Inventory
- A **flight search interface** - an attacker (or competitor/unauthorized travel agency) could leverage web scraping to scrape flight pricing to discover reverse engineer utilization.

We will be using the F5 Distributed Cloud Bot Protect service to protect the F5 airlines website.

Lab 1: Logging into F5 XC Console
=================================

During the first lab you will sign up for and subscribe to F5XC Platform

Lab 2: Exploiting automated threats against F5 Airlines
=======================================================

During this lab you will be running automated attacks against the F5 Airline web presence in order to understand the tactics and techniques leveraged by adversaries.

We will be using the F5 Automation Lab UDF image to exploit the following scenarios:

- Credential Stuffing (OAT-008_) attack against the F5 airlines login form - Using automation to validate a list of stolen credentials found on the darknet attempting to identify users who have used the same username and password on the F5 Airlines web portal - with the intention of stealing frequent flyer points.
- Card Cracking (OAT-010_) attack against the F5 airline credit card portal - Using automation to validate a list of stolen credit card numbers by attempting to process a very small transaction with each.
- Scraping (OAT-011_) attack against the F5 airline flight seasrch interface - Using automation to scrape flight pricing.

Lab 3: Protecting F5 Airlines using F5 Distributed Cloud Bot Protect 
====================================================================

In this lab we will configure F5 XC Bot Protect to protect the F5 Airlines web application backend (https://airline-backend.f5se.com)

Lab 4: Attempt to use automation tools against the protected website
===================================================================

This lab will explore the use of some of the automation tools like Selenium

Lab 5: Review F5 XC Bot Protect Reporting
=========================================

F5XC Bot Protect reporting is explored in this lab

Next: |signup|

.. |signup| raw:: html

            <a href="https://github.com/f5devcentral/f5-waap/blob/main/step-1-signup-deploy/voltConsole.rst" target="_blank">Lab 1: Sign Up for F5XC Platform</a>
