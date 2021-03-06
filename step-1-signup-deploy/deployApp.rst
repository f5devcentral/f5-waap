Deploy F5XC Microservices Demo App
==================================

    .. note:: F5 employees using F5-managed tenant should skip the steps below and instead use the deployed app running in "demo-app" namespace

#. Delegate DNS domain to F5XC by navigating to ``DNS Management`` -> ``Add Delegated domain``

#. Deploy F5XC Microservices Demo App by cloning and following steps in https://github.com/f5devcentral/volt-demo-app repo.

   #. Create API certificate file by clicking on ``Account Settings`` -> ``Credentials`` -> ``Create credentials``

      #. Fill out the details and select "API Certificate" as a Credential type 

         .. image:: ../_static/create_api_cert.png
   #. Build the traffic gen container using provided Dockerfile and push it to private registry. 
   #. Update variables in https://raw.githubusercontent.com/f5devcentral/volt-demo-app/main/terraform/variables.tf 
   #. Run "terraform init" followed  by "terraform apply" which will create necessary infrastructure in F5DC and deploy the F5XC Microservices Demo App along with traffic gen container

Next: |waf-lab|

.. |waf-lab| raw:: html

            <a href="https://github.com/f5devcentral/f5-waap/blob/main/waf-lab/waf-lab.rst" target="_blank">WAF lab: Protect F5XC Microservices Demo App</a>
