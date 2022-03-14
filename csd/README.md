# F5 Distributed Cloud Client-Side Defense Lab 

# Prerequisites
1. An account for F5 Distributed Cloud and a tenant with Client-Side Defense add-on capability provisioned.
2. An application which is accessible via the internet and where you can add the JavaScript the website. Alternativeley you can find instructions how to inject the JavaScript for testing purposes with the Chrome browser.
For *F5 SEs* the JavaScript was already added to the demo application and you can find the detais and login instructions for the f5-sales-demo tenant in the lab. 

<br>

You can sign up for a free account for the F5 Distributed Cloud in case you don't have an account yet by following the [sign up description](https://github.com/f5devcentral/f5-waap/blob/main/step-1-signup-deploy/voltConsole.rst) or just go directly to the [sign up page](https://console.ves.volterra.io/signup/usage_plan).
<br>

Please contact your F5 Sales Engineer/Account Manager for more information and please send any feedback for this lab to a.vistola@f5.com

<br>

# What we'll learn

During this hands-on lab you will learn about the following: 

- How to log into the F5 XC Console
- High level introduction in the use case of Client Side Defense (CSD)
- Configure CSD, logging and add the JavaScript to the web server
- Check if the telemetry data are sent to F5
- Using the Client Side Defense dashboard to mitigate suspicious domains
- Show that requests to suspicious domains are blocked

<br> 

## Lab Environment

During this lab you will be using the shared F5XC `f5-sales-public` tenant (the first lab exercise will cover how to access this environment). We will be setting up F5XC Client Side Defense in front of our sales-demo-app web site https://shop.sales-demo.f5demos.com/

<br> 

## Our Demo App - Sales-Demo

In this lab we will be protecting our sales-demo app. - You can explore the website by navigating to https://shop.sales-demo.f5demos.com/

<br> 

**Start the intro** by navigating to [Client Side Defense Lab](start-csd-intro.rst)

<br>

## Support
For support, please open a GitHub issue.  Note, the code in this repository is community supported and is not supported by F5 Networks.  For a complete list of supported projects please reference [SUPPORT.md](SUPPORT.md).

## Community Code of Conduct
Please refer to the [F5 DevCentral Community Code of Conduct](code_of_conduct.md).


## License
[Apache License 2.0](LICENSE)

## Copyright
Copyright 2014-2021 F5 Networks Inc.


### F5 Networks Contributor License Agreement

Before you start contributing to any project sponsored by F5 Networks, Inc. (F5) on GitHub, you will need to sign a Contributor License Agreement (CLA).

If you are signing as an individual, we recommend that you talk to your employer (if applicable) before signing the CLA since some employment agreements may have restrictions on your contributions to other projects.
Otherwise by submitting a CLA you represent that you are legally entitled to grant the licenses recited therein.

If your employer has rights to intellectual property that you create, such as your contributions, you represent that you have received permission to make contributions on behalf of that employer, that your employer has waived such rights for your contributions, or that your employer has executed a separate CLA with F5.

If you are signing on behalf of a company, you represent that you are legally entitled to grant the license recited therein.
You represent further that each employee of the entity that submits contributions is authorized to submit such contributions on behalf of the entity pursuant to the CLA.