Manage Suspicious Domains in Client Side Defense
================================================

Lab 1: Configure CSD and add the JavaScript to the web server
-------------------------------------------------------------

 .. note:: CSD leverages sampling, which means

1. Login
 
 Navigate to https://www.f5.com/cloud, select login at the top right and finally select your account type to login.

 .. note:: You can sign up for a free account for the F5 Distributed Cloud in case you don't have an account yet by following the `sign up description <https://github.com/f5devcentral/f5-waap/blob/main/step-1-signup-deploy/voltConsole.rst>`_ or just go directly to the sign up page https://console.ves.volterra.io/signup/usage_plan.

 .. image:: ../_static/csd-login.png

|

2. Enable CSD

 Once you logged in, click on "Client-Side Defense"

 .. image:: ../_static/csd-all-services.png

|

 And enable Client-Side Defense.

 .. image:: ../_static/csd-enable.png

|

3. Add the JavaScript to the web server

 Click on "Configuration" - "How to Inject JS" and follow step *1 - 3* on the right for adding the JavaScript to the web server between the <head> and </head> tags. Step 4 - 5 is explained below.

 .. image:: ../_static/csd-script.png

 After you have added the JavaScript to the web server, continue with step 4 from the screenshot above with adding the domain to protect, in our example f5demo.com.
 
 Finally proceed with step 5 from the screenshot  and finally use the 


 .. note:: These 5 steps were done already on the demo-app https://shop.sales-demo.f5demos.com hosted on the F5 Distributed Cloud.

 Please check this F5 internal channel for instructions on how to login to the `sales demo tenant
 <https://teams.microsoft.com/l/channel/19%3a45ba7ac2ebb540ecb3b44929aebd7e99%40thread.tacv2/Sales%2520Demo%2520Tenant%2520Account%2520Details?groupId=2dc42443-8b46-4694-aa58-defbd3dc8a4b&tenantId=dd3dfd2f-6a3b-40d1-9be0-bf8327d81c50/>`_.

|

4. Check if the telemetry data are sent to F5.

 Start the browser's Dev tools, filter for "oob" and reload the page until you see a similar POST request as below. This indicates that the telemetry data, collected by the JavaScript, are sent to F5.

  .. image:: ../_static/csd-filter-oob.png
 




 .. note:: CSD leverages sampling, which means

