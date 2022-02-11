Sign-up for F5 WAAP Service
===========================


Customers and partners can use self-service sign-up option to create Free/Individual/Teams level tenants. 

#. To sign-up navigate to |f5dc| and click ``Sign up`` 

   .. image:: ../_static/volterra_io.png

#. Then select the account type (Free/Individual/Teams) and click ``Next``
#. Provide your Email and click ``Next``

   .. image:: ../_static/volterra_email.png

#. Fill out personal details form and click  ``Next`` or ``Create account`` depending on the account level i.e. Individual/teams level accounts have an extra step to provide a payment method

   .. note:: Organization-level accounts ("Organization Plan") can be requested by contacting the F5 Sales or Account team

Logging into F5 Distributed Cloud Console
=========================================


Login to F5 Distributed Cloud Console
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You should have received an email with an invitation to access F5 Distributed Cloud Console.
You will need to create a password that will be associated with your email address.

If you have NOT received an email from our system you may need to provide an alternate
email address that we can use for the purposes of this lab.

Free/Individual accounts login uses Email/Password whereas Team/Organization accounts may use Email/Password or SSO options.

   .. image:: ../_static/volterra_login.png

**F5 Distributed Cloud Console**

F5 Distributed Cloud Console is a SaaS control-plane for Distributed Cloud Platform services that provides a UI and API for managing network, security, and compute services.

Using F5 Distributed Cloud Console, an end-user can centrally manage distributed application environments and Platform services.

Terminology
~~~~~~~~~~~~~

Namespace
    Namespace is a term that is commonly used in Kubernetes.  It can be thought of as a grouping of resources.

Select your Persona
~~~~~~~~~~~~~~~~~~~

#. Log into F5 Distributed Cloud Platform tenant. F5 SEs should use their assigned tenant i.e. https://f5-sales-public.console.ves.volterra.io/

    .. note:: The F5 Distributed Cloud Console GUI has a relatively short timeout. This is not configurable. We have an enhancement request to allow this to be configured.

#. When you first login you will need to select your "persona"

   Enter your persona as "SecOps" and level as "Intermediate".  You can change these settings after logging in as well.

   Your persona will highlight workflows within F5 Distributed Cloud Platform.  You will be able to access all services, but making use of
   personas can focus your view on particular tasks that are relevant to your role.

#. Several tooltips will appear.  You can close these out.

Identify or create your Namespace
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

F5 employees
~~~~~~~~~~~~
#. Click on "Account Settings" by expanding the "Account" icon in the top right of the screen and 
   clicking on "Account Settings"

   .. image:: ../_static/screenshot-account-settings.png
#. Next click on "My Namespaces" and take note of the `yourName` namespace that you have been assigned. For example, John Smith's namespace would be created as "j-smith"

   .. image:: ../_static/j-smith.png 

F5 customers
~~~~~~~~~~~~

#. Click on "Account Settings" by expanding the "Account" icon in the top right of the screen and 
   clicking on "Account Settings"

   .. image:: ../_static/screenshot-account-settings.png

#. Next click on ``My Namespaces`` -> ``Add namespace``. Fill out "Name" field and optionally assign users and explicit roles for the new namespace. Click "Save changes"

   .. image:: ../_static/volterra_create_ns.png


Next: |deploy-app|

.. |deploy-app| raw:: html

            <a href="https://github.com/f5devcentral/f5-waap/tree/main/step-1-signup-deploy/deployApp.rst" target="_blank">Deploy F5XC Microservices Demo App</a>


.. |f5dc| raw:: html

            <a href="https://volterra.io" target="_blank">F5 Distributed Cloud Platform</a>