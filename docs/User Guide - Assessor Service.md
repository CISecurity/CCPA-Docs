CIS-CAT Pro Assessor Service User Guide
=====================================

![](http://i.imgur.com/5yZfZi5.jpg)


Introduction
------------
CIS-CAT Pro Assessor v4 Service is a Web service version of CIS-CAT Pro Assessor v4.  It provides REST APIs in the form of URLs that call specific Assessor v4 functionality.  Responses to the calling client are in JSON format.  CIS-CAT Pro Assessor v4 Service is designed to interact with the CIS-CAT Pro Dashboard v1.1.11+ to allow configuration assessments to be run from CIS-CAT Pro Dashboard against a specified target system.

## Host Machine Requirements ##
The Host machine is the machine where CIS-CAT Pro Assessor v4 Service resides. Any operating system can support CIS-CAT Pro Assessor v4 Service provided the system can run Java.

To support the broadest possible portability, CIS-CAT Pro Assessor v4 Service is a Java application and requires an available Java Runtime Environment (JRE) to execute on the host machine. The following components are required to run CIS-CAT Pro Assessor v4 Service.
To allow the greatest flexibility for configuring server performance, CIS highly recommends installing CIS-CAT Pro Assessor v4 Service on a host separate from hosts supporting CIS-CAT Pro Dashboard.


- Java 8+ installed on host or accessed via a network share
- OpenJDK implementations of 8 or higher are supported. See https://openjdk.java.net/ for information about these free and open-source implementations of Java.
- HTTPS communication protocol between Assessor Service host and Dashboard (highly recommended)
- CIS-CAT Pro Dashboard v1.1.11+


##Benchmark Coverage##
CIS-CAT Pro Assessor v4 Service supports all CIS benchmarks included with CIS-CAT Pro Assessor v4, except for those that require interactive values. Interactive Benchmarks can be reviewed here: https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/.

## Deployment ##
Obtain the latest CIS-CAT Pro Assessor v4 Service from the [CIS WorkBench](https://workbench.cisecurity.org/files). Use the tag `CIS-CAT` to filter the results in the Downloads section of CIS WorkBench. 

1. Unzip the downloaded bundle in the desired host machine folder
2. Configure the **assessor-service.properties** and **server.conf** files located in the **"config"** folder.  See the **Configuration** section below for details.
3. Start the application by executing scripts as a root, administrator, or equivalently privileged principal
	- Open a command prompt "as an administrator"
	- For Microsoft Windows hosts, execute **Assessor-Service.bat**
	- For Unix/Linux hosts, execute **Assessor-Service.sh**

## Configuration ##
		

### Configure Assessor Service Properties ###
CIS-CAT Pro Assessor v4 Service includes a properties file located in the “config” folder where default options can be configured. The file is called **assessor-service.properties**.  This file is similar to the CIS-CAT Pro Assessor v4 properties file. Below are the key properties to be configured for CIS-CAT Pro Assessor v4 Service.

| Property                         | Description                                   |
| -------------------------------- | --------------------------------------------- |
| produce.assessment.output.files  | By default, this feature is turned off and set to the recommended ‘false’ value. If set to ‘true’, every target system assessment will produce a detailed runtime log in the "logs" folder.  Although useful for debugging and troubleshooting, CIS recommends leaving this property set to 'false' as it may consume excessive disk space.
| ciscat.post.parameter.ccpd.token | CIS-CAT Pro Dashboard generated token. The same token can be used from existing CIS-CAT Pro Assessor v4 assessor-cli.properties file. See CIS-CAT Pro Dashboard documentation for more information on generating a token. |




### Configure HTTPS Protocol ###
It is highly recommended that communication between CIS-CAT Pro Dashboard and CIS-CAT Pro Assessor v4 Service occur using HTTPS protocol. The CIS-CAT Pro Dashboard deployment guide contains a guide on securing Web traffic using HTTPS supported by certificates. However, there are many methods for creating/obtaining a certificate. For use with Assessor Service, any method may be selected as long as the method chosen uses the **RSA algorithm** with a **keysize of 2048** to generate the certificate.

#### Example Certificate Generation Method ####

See an [example](https://docs.oracle.com/cd/E54932_01/doc.705/e54936/cssg_create_ssl_cert.htm#CSVSG181) for creating a self-signed certificate.

The following steps provide a simple way to generate a self-signed SSL certificate for use by the embedded Jetty server using the keytool command on Windows, Mac, or Linux:

1. Open a command prompt or terminal "as an Administrator"
2. Navigate to the desired folder where keystore will be created to store self-signed certificate
3. Run below command `keytool -keystore <keystore_name.jks> -alias <certificate_alias> -keyalg RSA -keysize 2048 -sigalg SHA256withRSA -genkey -validity <days>`
	- keystore_name.jks = name of created keystore
	- certificate_alias = alias name of self-signed certificate created, used for `server.ssl.certificate.alias` property
	- days = desired number of days certificate will be valid 
4. Enter password for keystore. 
5. Re-enter the password when prompted. 
6. Store password in `server.ssl.keystore.password` property.
7. When prompted for a first and last name, enter the domain name of the server. For example, *myserver* or *myserver.mycompany.com*.  This is the “common name” used to identify your server and associate it with the self-signed certificate.
8. Enter the other details, such as Organizational Unit, Organization, City, State, and Country
9. Confirm information by entering "yes"
10. When prompted with "Enter key password for <certificate_alias>”, press Enter to use the same password as the keystore password or enter a different password.
11. Store this password in `server.ssl.key.password` property
12. Run command to verify contents of keystore 
	`keytool -list -v -keystore <keystore_name.jks>`
13. When prompted, enter the keystore password created above
14. From basic, generated certificate information displayed, verify "Owner" = "Issuer"
15. Ignore the warning about JKS being a proprietary keystore

### Configure Assessor Service Communication Properties ###
CIS-CAT Pro Assessor v4 Service includes a properties file used exclusively for setting properties utilized for configuring the embedded Web server. The file is in the “config” folder and is called **server.conf**. Use the information from the certificate generation process to set the property values below.

**IMPORTANT:**  The **server.conf** file contains sensitive data.  This file is used to configure the embedded Web server when starting the CIS-CAT Pro Assessor v4 Service application, but it is not needed after startup.  As such, CIS recommends storing this file in a secure location after the application has been successfully started. 


| Property                         | Description                                        |
| -------------------------------- | -------------------------------------------------- |
| server.http.port  | The listening port for Web service requests from CIS-CAT Pro Dashboard. Default is set to 8080. HTTP is NOT recommended when CIS-CAT Pro Assessor v4 Service resides on a separate host than CIS-CAT Pro Dashboard Web server.
| server.https.port | The listening port for Web service requests from CIS-CAT Pro Dashboard. Default is set to 443. 
| server.ssl.keystore.location | Sets the full path and file name to the location of the keystore for HTTPS connections. 
| server.ssl.keystore.password | Sets the password of the keystore used for HTTPS connections. 
| server.ssl.certificate.alias | Sets the alias of the public certificate used for HTTPS connections. Currently should be set to “Jetty”. 
| server.ssl.ignore.certificate.warnings | Indicates if HTTPS requests sent to the CIS-CAT Pro Dashboard should ignore an SSL certificate warnings. |

### Configure CIS-CAT Pro Dashboard for Assessment ###
See the CIS-CAT Pro Dashboard instructions for configuration instructions that enable features to orchestrate assessments from the GUI.



