Lab 3: Protecting F5 Airlines using F5 Distributed Cloud Bot Protect 
====================================================================

In this lab we will configure F5 XC Bot Protect to protect the F5 Airlines web application backend (https://airline-backend.f5se.com)

There are two phases

1. Getting the traffic flowing via F5 XC 
2. Configuration of the F5 XC Bot Protect capability to protect the endpoints.

Note: There are two layers of bot protection available in F5 XC:

 - Basic signature based bot protection - configured as part of the App Firewall object.

 .. image:: /_images/botprotect1.png


 - Advanced Bot Protection - configured as part of the Load Balancer object which includes sophisticated signal collection / capabilities for dealing with advanced/targeted adversaries\
   
 .. image:: /_images/botprotect2.png


For the puprose of today's lab we will be configuring Advanced Bot Protection.

.. toctree::
   :maxdepth: 1
   :caption: Contents:

   lbsetup
   botsetup


