F5 Distributed Cloud Bot Protect 101
====================================

`Last updated: 2022-02-02 2:00 PM AEST`

F5 Distributed Cloud Bot Protect protects your web properties from automated attacks by identifying and mitigating malicious bots and abuse as a result of automation. F5 Distributed Cloud Bot Protect brings Shape Security's industry leading efficacy to the F5XC platform.

Web security is no longer constrained to inadvertent vulnerabilities.​
​
Attackers are abusing inherent functionality to conduct automated and manual fraud.

Examples of common automated threats include:

- OAT-001_ Carding
- OAT-002_ Token Cracking
- OAT-003_ Ad Fraud
- OAT-004_ Fingerprinting
- OAT-005_ Scalping
- OAT-006_ Expediting
- OAT-007_ Credential Cracking
- OAT-008_ Credential Stuffing
- OAT-009_ CAPTCHA Defeat
- OAT-010_ Card Cracking
- OAT-011_ Scraping
- OAT-012_ Cashing Out
- OAT-013_ Sniping
- OAT-014_ Vulnerability Scanning
- OAT-015_ Denial of Service
- OAT-016_ Skewing
- OAT-017_ Spamming
- OAT-018_ Footprinting
- OAT-019_ Account Creation
- OAT-020_ Account Aggregation
- OAT-021_ Denial of Inventory

For more information about common automated threats/abuse as a result of bots/automation .. _please refer to the OWASP guide to Automated Threats to Web Applications. https://owasp.org/www-project-automated-threats-to-web-applications/

Advesary Arms Race
------------------

There are many different techniques that can be utilized to differenciate between a real and legitimate human/customer accessing a web prescence and an advesary leveraging automation to exploit an automated threat class - each with it's own level of efficacy, user impact and friction.

Some common techniques include:

- Identifying bots using signatures that match the request characteristics of a bot (i.e. Useragent string - This technique can be trivially bypased by an advesary by altering their requests to look like requests from legitimate browsers (changing the useragent to a legtimate browser UA etc)
- Making users solve a CAPCHA (Capcha's introduce friction for users and are ineffective in that they can be solved in some cases by using OCR, in other cases by integrating with a cacpcha solving services such as 2capcha)
- Sending a javascript based challenge to the client (Javascript based challenges can vary significantly in efficacy - Advesaries can leverage automation tools with javascript based execution environments (i.e. PhantomJS and Selenium Webdriver) to solve javascript based challenges or break the obfuscation of javascript and reverse engineer a solution to the challenge)

Based on observed adversary behaviour an arms race exists - There is inherant value that the attacker is looking to extract as a result of their use of automated threat techniques - as a result advesaries quickly adapt and retool as more sophisticated anti-automation techniques are deployed. 

Identifying the most sophisticated advesaries exploiting automated threats is challenging -  F5 Distributed Cloud's Bot Protect capability provides very high efficacy against the most sophisticated advesaries - providing a determanistic (is it a bot or not a bot - not a risk score), low friction (doesnt introduce CAPCHA or other techniques to differenciate humans/bots) and highly effective tactics against advesaries that retool/attempt to defeat the service.

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
- A **credit card payment gateway** - an attacker could use automation to test a large numbner of stolen credit cards - an example of OAT-010 Card Cracking
- A **frequent flyer gift card system** - an attacker could use automation to brute force gift card IDs and PINs - an example of OAT-002 Token Cracking
- A **flight booking interface** - an attacker could use automation to block/hold all the seats on a flight - an example of OAT-021 Denial of Inventory
- A **flight search interface** - an attacker (or competitor/unauthorized travel agency) could leverage web scraping to scrape flight pricing to discover reverse engineer utilization.

We will be using the F5 Distributed Cloud Bot Protect service to protect the F5 airlines website.

.. toctree::
   :maxdepth: 1
   :caption: Contents:

   lab1/index
   lab2/index
   lab3/index
   lab4/index
   lab5/index
