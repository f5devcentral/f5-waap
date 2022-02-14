Lab 4: Attempt to use automation tools againt the protected website
===================================================================

#. Log into the UDF blueprint "Athena Attacker" - "Launchpad" Windows image using the credentials in the UDF documentation tab.

 .. image:: _images/validate1.png

#.  Open PyCharm from the UDF windows system's desktop.

 .. image:: _images/validate2.png

#. Update the target variable definition replacing https://airline.f5se.com/user/signin with http://<cname-name>/user/signin (Replace <cname-name> with the CNAME copied from the load balancers screen)

 .. image:: _images/validate3.png

#. Click the run icon to run the credential stuffing attack using Selenium driver against the protected site.

 .. image:: _images/validate4.png



Next: |bot-lab5| 

.. |bot-lab5| raw:: html

            <a href="https://github.com/f5devcentral/f5-waap/tree/main/bot-lab/lab5.rst" target="_blank">Lab 5: Review F5XC Bot Protect Reporting</a>
