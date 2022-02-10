Deploy Hipster App
===================

#. Delegate DNS domain to F5DC by navigating to "DNS Management" -> "Add Delegated domain"

#. Deploy Hipster App by cloning and following steps in https://github.com/f5devcentral/volt-demo-app repo.

   #. Create API certificate file by clicking on "Account Settings" -> "Credentials" -> "Create credentials"

      #. Fill out the details and select "API Certificate" as a Credential type 

         .. image:: ../_static/create_api_cert.png
   #. Build the traffic gen container using provided Dockerfile and push it to private registry. 
   #. Update variables in https://raw.githubusercontent.com/f5devcentral/volt-demo-app/main/terraform/variables.tf 
   #. Run "terraform init" followed  by "terraform apply" which will create necessary infrastructure in F5DC and deploy the Hipster App along with traffic gen container

Next: |waf-lab|

.. |waf-lab| raw:: html

            <a href="https://github.com/f5devcentral/f5-waap/tree/main/waf-lab" target="_blank">Protect Hipster App</a>
