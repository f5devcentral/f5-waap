Lab 2 - Part 2  : Running a credential stuffing attack against F5 airlines
==========================================================================

Lab 2 - Part 2: Exercise 1: Credential Stuffing with OpenBullet 2
-----------------------------------------------------------------

OpenBullet 2 (https://github.com/openbullet/OpenBullet2) is a cracking tool often utilised by skript kiddies to target online presences with brute force/credential stuffing attacks

In this exercise we will be using OpenBullet 2 to validate a combo list (username and password credentials list) against the unprotected F5 airlines backend. In subsequent modules we will protect the airline application using F5 XC Bot Protect and re run these attacks.

1. To run OpenBullet, double click on the openbullet icon on the desktop of the "Launchpad" windows system as part of the "Athena Attacker Blueprint"
 .. image:: /_images/credstuff1.png

2. After a short time the OpenBullet app wil load 
 .. image:: /_images/credstuff1.1.png

3. Click on the configs button
 .. image:: /_images/credstuff2.png

4.  Edit the airlinestuff-backend config by selecting it and clicking the edit button.
 .. image:: /_images/credstuff3.png

5. Review the Http request block by clicking on it - Note that it is configured to POST credentials to /user/signin using the form post method.
 .. image:: /_images/credstuff4.png

6. Review the Keycheck block by clicking on it - Note that it is looking for the string "Successfully signed in." in the pagee in order to identify a successful username/password combo.
 .. image:: /_images/credstuff5.png

7. Review the wordlists tab - This is where the user specifies the credential combo lists to be attempted. We have configured a short list of combos entited "creds.wordlist"
 .. image:: /_images/credstuff6.png

8. Ok - lets run an attack - Click on the jobs tab and click "New"
 .. image:: /_images/credstuff7.png

9. Select a "Multi run" job type in order to run a credential stuffing attack with our credentials database against the F5 Airlines backend
 .. image:: /_images/credstuff8.png

10. Click on the "Select Config" button to open the configuration selection screen
 .. image:: /_images/credstuff9.png

11. select the "airlinestuff-backend" button and select our configuration and accept.
 .. image:: /_images/credstuff10.png

12. Click on the "Select wordlist" button to select the combo list for this attack
 .. image:: /_images/credstuff11.png

13. Select our "Creds.wordlist" wordlist and click accept 
 .. image:: /_images/credstuff12.png

14. Click "Accept" to save the multi-run job and our job will now be visible in the jobs list 
 .. image:: /_images/credstuff13.png

15. Double click on the job we created:
 .. image:: /_images/credstuff14.png

16. Click start and the credential stuffing attack will start - Each of the credentials will be validated against the login form.
 .. image:: /_images/credstuff15.png

17. Note that we were able to identify a credential that was sucessful against the airline backend


Lab 2 - Part 2: Exercise 2: Credential Stuffing with Selenium Webdriver
-----------------------------------------------------------------------

Selenium Webdriver (https://www.selenium.dev/) is a framework for browser automation commonly utilised for creating test automation, but is also often utilised by advesaries who want to defeat simple anti-automation controls that rely on request/UA analysis, javascript based challenges etc.  Selenium WebDriver provides a programatic SDK for interfacing and driving the web browser.

In this exercise we will be using the python requests library - a simple HTTP client (that doesnt inject javascript) that can be used to generate requests and inspect responses within python3 in order to scrape flight pricing from the F5 airlines web channel.

1. In the UDF environment, Open the PyCharm python IDE
 .. image:: /_images/selenium1.png

2. Review the python code - it:
   
 - Initialises the chrome selnium Webdriver
 - Iterates through a CSV file of stolen credentials attempting each username and password combination until it finds a successfull combo.

 .. image:: /_images/selenium2.png

1. Run the python code by clicking the run icon
 .. image:: /_images/selenium3.png

4. Note the credential stuffing attack.
 .. image:: /_images/selenium4.png

5. The webdriver will automate chrome's interaction with the F5 Airlines site - attempting all the username/password combinations in the credentials database until a successful username/password combinaton is found.