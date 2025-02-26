<a href="http://wso2.com/products/identity-server/">
<img src="http://b.content.wso2.com/sites/all/common/images/product-logos/identity-server.svg"
     srcset="http://b.content.wso2.com/sites/all/common/images/product-logos/identity-server.svg@2x.png 2x"
     alt="WSO2 Identity Server" />
</a>

# Welcome to WSO2 Identity Server

|  Branch | Build Status | Test Results |
| :------------ |:------------- |:-------------
| master      | [![Build Status](https://wso2.org/jenkins/job/products/job/product-is/badge/icon)](https://wso2.org/jenkins/job/products/job/product-is/) | [![Test Results](https://wso2.org/jenkins/job/products/job/product-is/badge/icon)](https://wso2.org/jenkins/job/products/job/product-is/lastBuild/testReport/) |


[![Stackoverflow](https://img.shields.io/badge/Ask%20for%20help%20on-Stackoverflow-orange)](https://stackoverflow.com/questions/tagged/wso2is)
[![Discord](https://img.shields.io/badge/Join%20us%20on-Discord-%23e01563.svg)](https://discord.gg/wso2)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/wso2/product-is/blob/master/LICENSE)
[![Twitter](https://img.shields.io/twitter/follow/wso2.svg?style=social&label=Follow)](https://twitter.com/intent/follow?screen_name=wso2)
---

WSO2 Identity Server is an open source Identity and Access Management solution federating and managing identities across 
both enterprise and cloud service environments. It supports a wide array of authentication 
protocols such as SAML 2.0 Web SSO, OpenID, OAuth 2.0, OpenID Connect and WS-Federation Passive. 
It supports role based authorization and fined grained authorization with XACML 2.0/3.0 while inbound/outbound provisioning is 
supported through SCIM.

This is based on the revolutionary WSO2 Carbon framework. All the major features have been developed as pluggable Carbon components.

System Requirements
===================

1. Minimum memory - 2 GB

2. Processor - 2 Core/vCPU 1.1GHz or higher

3. Java SE Development Kit 11

4. The Management Console requires full Javascript enablement of the Web browser.

5. To build WSO2 Identity Server from the Source distribution, it is also necessary that you have Maven 3 or later.

For more details see
   * https://is.docs.wso2.com/en/7.1.0/deploy/get-started/install/ (For IS 7.1.0 version)

Project Resources
=================

* Home page          : http://wso2.com/products/identity-server
* Library            : https://wso2.com/library/identity-and-access-management
* Wiki 
    * IS 7.1.0 version     : https://is.docs.wso2.com/en/7.1.0/
* Issue Tracker      : https://github.com/wso2/product-is/issues      
* Forums             : http://stackoverflow.com/questions/tagged/wso2is/
* IAM Developer List: iam-dev@wso2.org


Building the distribution from source
=========================================

1. Install Java SE Development Kit 11
2. Install Apache Maven 3.x.x(https://maven.apache.org/download.cgi#)
3. Get a clone from https://github.com/wso2/product-is.git or download the source 
4. Run the one of the below maven commands from product-is directory, 
    - `mvn clean install` (To build the binary and source distributions with the tests)
    - `mvn clean install -Dmaven.test.skip=true` (To build the binary and source distribution, without running any of 
    the unit/integration tests)
5. You can find the binary distribution in `product-is/modules/distribution/target` directory.

    
Installation and Running
========================

1. Extract the downloaded/built binary distribution zip file
2. Run the wso2server.sh or wso2server.bat file in the /bin directory
3. Once the server starts, point your Web browser to https://localhost:9443/carbon/
4. Developer and Administrator Console is available at https://localhost:9443/console
5. End User Portal is available at https://localhost:9443/myaccount
6. For more information, see the Installation Guide


WSO2 Identity Server Distribution Directory Structure
==============================================

            CARBON_HOME
            ├── bin
            ├── dbscripts
            ├── lib
            ├── repository
            │   ├── components
            │   ├── conf
            │   │   └── identity
            │   │       ├── identity-providers
            │   │       └── service-providers
            │   ├── database
            │   ├── deployment
            │   ├── logs
            │   ├── resources
            │   │   ├── identity
            │   │   └── security
            │   └── tenants
            └── tmp


    - bin
      Contains various scripts .sh & .bat scripts.

    - dbscripts
      Contains the database creation & seed data population SQL scripts for
      various supported databases.

    - lib
      Contains the basic set of libraries required to startup Carbon.

    - repository
      The repository where Carbon artifacts & Axis2 services and 
      modules deployed in WSO2 Carbon are stored. 
      In addition to this other custom deployers such as
      dataservices and axis1services are also stored.

        - components
          Contains all OSGi related libraries and configurations.

        - conf
          Contains server configuration files. Ex: axis2.xml, carbon.xml

	        - identity
	          Contains all configurations related to identity.

	            - identity-providers
	              Identity providers configured using file

	            - service-providers
	              Service providers configured using file

        - database
          Contains the WSO2 Registry & User Manager database.

        - deployment
          Contains server side and client side Axis2 repositories. 
	      All deployment artifacts should go into this directory.

        - logs
          Contains all log files created during execution.

        - resources
          Contains additional resources that may be required.

	- tenants
	  Directory will contain relevant tenant artifacts 
	  in the case of a multitenant deployment.

    - tmp
      Used for storing temporary files, and is pointed to by the
      java.io.tmpdir System property.


    - LICENSE.txt
      Apache License 2.0 under which WSO2 Carbon is distributed.

    - README.txt
      This document.

    - release-notes.html
      Release information for WSO2 Carbon ${carbon.product.version}.

Secure sensitive information in carbon configuration files
----------------------------------------------------------

There are sensitive information such as passwords in the carbon configuration. 
You can secure them by using secure vault. Please go through following steps to 
secure them with default mode. 

1. Configure secure vault with default configurations by running ciphertool 
	script from bin directory.  

> ciphertool.sh -Dconfigure   (in UNIX)  

This script would do following configurations that you need to do by manually 

(i) Replaces sensitive elements in configuration files,  that have been defined in
		 cipher-tool.properties, with alias token values.  
(ii) Encrypts plain text password which is defined in cipher-text.properties file.
(iii) Updates secret-conf.properties file with default keystore and callback class. 

cipher-tool.properties, cipher-text.properties and secret-conf.properties files 
			can be found at repository/conf/security directory. 

2. Start server by running wso2server script from bin directory

> wso2server.sh   (in UNIX)

By default mode, it would ask you to enter the master password 
(By default, master password is the password of carbon keystore and private key) 

3. Change any password by running ciphertool script from bin directory.  

> ciphertool -Dchange  (in UNIX)

For more details see
https://is.docs.wso2.com/en/7.1.0/deploy/security/encrypt-passwords-with-cipher-tool/

Support
=======
We are committed to ensuring that your enterprise middleware deployment is completely supported from
evaluation to production. Our unique approach ensures that all support leverages our open development
methodology and is provided by the very same engineers who build the technology.

For more details and to take advantage of this unique opportunity, visit http://wso2.com/support/.


For more information on WSO2 Carbon, visit the WSO2 Oxygen Tank (http://wso2.org)

For more information about WSO2 Identity Server please see http://wso2.org/projects/identity or visit the
WSO2 Oxygen Tank developer portal for addition resources.

For further details, see the WSO2 Carbon documentation at
https://docs.wso2.com/display/Carbon4411/WSO2+Carbon+Documentation

Survey On Open Source Community Communication
=============================================

WSO2 wants to learn more about our open source software (OSS) community and your communication preferences to serve you better.

In addition, we may reach out to a small number of respondents to ask additional questions and offer a small gift.

Link to survey: https://forms.gle/h5q4M3K7vyXba3bK6


---------------------------------------------------------------------------
(c) Copyright 2022 WSO2 LLC.
