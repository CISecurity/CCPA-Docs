CIS-CAT Pro Assessor Service User Guide
=====================================

![](http://i.imgur.com/5yZfZi5.jpg)


Introduction
------------
CIS-CAT Pro Assessor v4 Service is a Web service version of CIS-CAT Pro Assessor v4.  It provides REST APIs in the form of URLs that call specific Assessor v4 functionality.  Responses to the calling client are in JSON format.  CIS-CAT Pro Assessor v4 Service is designed to interact with the CIS-CAT Pro Dashboard v1.1.11+ to allow configuration assessments to be run from CIS-CAT Pro Dashboard against a remote target system. This companion application works the same as CIS-CAT Pro Assessor v4 except that it does not have a CLI. This application can be used alone for Dashboard assessment requests or in conjunction with CIS-CAT Pro Assessor v4 for all other command line, local, or centralized scanning activities. 


## System Recommendations ##
The host system is the machine where CIS-CAT Pro Assessor v4 Service resides. Most operating system can support CIS-CAT Pro Assessor v4 Service provided the system can run Java. See below for an example implementation used in our testing labs. CIS-CAT Pro Assessor v4 Service is a Java application and requires an available Java Runtime Environment (JRE) to execute on the host system. 

To allow the greatest flexibility for configuring server performance, CIS recommends deploying CIS-CAT Pro Assessor v4 Service on a dedicated host separate from other hosts supporting CIS-CAT Pro Dashboard. Although a single scan is not expected to require a lot of processing power, future functionality such as the ability to schedule scanning of multiple target systems could.  

For implementations where CIS-CAT Pro Assessor v4 Service will be on a dedicated host, the following is required and recommended.

**Required:**

- CIS-CAT Pro Dashboard v1.1.11+ installed
- Any JRE version from 8 to 14 installed on host or accessed via a network share
  - [OpenJDK implementations](https://openjdk.java.net/) of Java supported

**Recommended:**

- 2 GHz dual processor*
- 4 GB of RAM*
- HTTPS communication protocol between Assessor Service host and Dashboard (highly recommended)

\*  These minimum host system recommendations are based on the assumption the Assessor Service will only be utilized for ad-hoc assessments initiated from the Dashboard.  If higher usage is anticipated, system specifications may need to be adjusted.

As an example, our test environment utilizes an AWS t2.large Ubuntu 18.04 instance, which has:

- 8GB RAM
- 2 vCPUs



## Deployment ##
Obtain the latest CIS-CAT Pro Assessor v4 Service from the [CIS WorkBench](https://workbench.cisecurity.org/files). Use the tag `CIS-CAT` to filter the results in the Downloads section of CIS WorkBench. Example instructions for host system configurations are below.

**Required:**

- Java 8 installed on host or accessed via a network share
- CIS-CAT Pro Dashboard v1.1.11+ installed
- Unrestricted communication (ports open and allowed with firewall management) between:
	- CIS-CAT Pro Dashboard and CIS-CAT Pro Assessor v4 Service
	- CIS-CAT Pro Assessor v4 Service and desired remote target systems
	- Remote target systems configured for remote assessment ([WinRM Setup](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#microsoft-windows-endpoint-configuration), [SSH enabled](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#unixlinuxosx-endpoint-configuration), etc.)



### Configure Assessor v4 Service on a Dedicated Server (Recommended)
This is the recommended configuration as secure credentials will be encrypted using standard HTTPS protocol.
 

1. Unzip the downloaded bundle in the desired host machine location
2. For automatic report upload to CIS-CAT Pro Dashboard, configure the **assessor-service.properties** file property ciscat.post.parameter.ccpd.token
	- Existing Dashboard and Assessor v4 authentication, copy the token that appears in the [API User within Dashboard](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#cis-cat-pro-assessor-integration)
	- New Dashboard and Assessor v4 authentication, follow [these instructions](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#cis-cat-pro-assessor-integration)
3. [Create an HTTPS certificate](https://ccpa-docs.readthedocs.io/en/latest/User%20Guide%20for%20Assessor%20Service/#create-https-certificate "Create HTTPS certificate") and make note of key information from certificate instructions
	- The information will be needed for the **server.conf** file located in the "config" folder
4. Configure the **server.conf** file located in the **"config"** folder.
5. Validate Java 8 is installed
6. Configure the [CIS-CAT Pro Dashboard ccpd-yml file](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#cis-cat-pro-assessor-v4-service-integration)
	- Ensure spacing and tabbing matches the examples very closely as yml files are particular with information "lining up"
7. Start the application by executing scripts as a root, administrator, or equivalently privileged principal
	- Open a command prompt "as an administrator"
	- For Microsoft Windows hosts, execute **Assessor-Service.bat**
	- For Unix/Linux hosts, execute **Assessor-Service.sh**
8. Restart the service anytime changes are made to the assessor-service.properties or server.conf file
9. Ensure target systems are configured for remote assessment. See [CIS-CAT Pro Assessor v4 Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#microsoft-windows-endpoint-configuration).
10. Review the [CIS-CAT Pro User Guide](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20User's%20Guide/#assess-a-target-system)
11. Once success is achieved, it is recommended to set the Assessor v4 Service up as a service on the host machine

### Configure Assessor v4 Service on CIS-CAT Pro Dashboard's Tomcat Host
Deployment of Assessor v4 Service to the Tomcat (a supporting component for CIS-CAT Pro Dashboard) host, although not the preferred option as it carries some risk, is also possible. When deploying to Tomcat, http communication is utilized. Most importantly, when deployed to the Tomcat Host, ensure that the port used for the Assessor v4 Service is different than the one the Dashboard uses and that the selected port is not in use for any other application. 


1. Unzip the downloaded bundle in the desired host machine location
2. For automatic report upload to CIS-CAT Pro Dashboard, configure the [**assessor-service.properties**](https://ccpa-docs.readthedocs.io/en/latest/User%20Guide%20for%20Assessor%20Service/#configuration) file property ciscat.post.parameter.ccpd.token
	- Existing Dashboard and Assessor v4 authentication, copy the token that appears in the [API User within Dashboard](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#cis-cat-pro-assessor-integration)
	- New Dashboard and Assessor v4 authentication, install Dashboard and [generate a token](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#cis-cat-pro-assessor-integration)
3. Configure the [**server.conf**](https://ccpa-docs.readthedocs.io/en/latest/User%20Guide%20for%20Assessor%20Service/#configuration) file located in the **"config"** folder.
5. Validate Java 8 is installed
6. Configure the [CIS-CAT Pro Dashboard ccpd-yml file](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#cis-cat-pro-assessor-v4-service-integration)
	- Avoid local port conflict by setting the assessor service to a different URL containing the local port in the ccpd-config.yml file
	- Avoid other application port conflict by selecting a port that is not used
	- Ensure the selected local port is available and open
	- Ensure spacing and tabbing matches the examples very closely as yml files are particular with information "lining up"
7. Start the application by executing scripts as a root, administrator, or equivalently privileged principal
	- Open a command prompt "as an administrator"
	- For Microsoft Windows hosts, execute **Assessor-Service.bat**
	- For Unix/Linux hosts, execute **Assessor-Service.sh**
8. Restart the service anytime changes are made to the assessor-service.properties or server.conf file
9. Ensure target systems are configured for remote assessment. See [CIS-CAT Pro Assessor v4 Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#microsoft-windows-endpoint-configuration).
10. Review the [CIS-CAT Pro User Guide](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20User's%20Guide/#assess-a-target-system)
11. Once success is achieved, it is recommended to set the Assessor v4 Service up as a service on the host machine

### Configure Assessor v4 Service as a Service
It is recommended to add Assessor v4 Service as a running service on the host machine of Assessor v4 Service. Below are example instructions on automating system tasks to ensure CIS-CAT Pro Assessor v4 Service is running during optimal times to support business processes. The instructions below have been tested on a Microsoft Windows 2019 server and an Ubuntu 16.04 and 18.04 server. Exact instructions may vary for each organization depending on the host machine of CIS-CAT Pro Assessor v4 Service or organizational policies and business processes.

**Windows**

1. Navigate to task scheduler and create a new task
2. On the General tab, select the option "Run whether user is logged in or not"
3. On the Triggers tab, add desired organizational triggers. For example:
	- select "New" and choose to begin the task at startup
1. On the Actions tab, select "New"
2. Navigate to and select the Assessor-Service.bat file in the Program/script field
3. Fill in "Start in" with the file path of the Assessor Service main folder structure
	- This is a mandatory, not optional as listed on the Windows screen
1. Close and save the task setup
2. Restart the host machine to verify successful service startup


	![](https://i.imgur.com/GTlpuW1.png)

**Linux**

1. Create a new file in /etc/systemd/system called AssessorService.service
2. Change the directory of WorkingDirectory and ExecStart to the location of where AssessorService is deployed
3. Paste the following into the above file:

	![](https://i.imgur.com/CxtZjU3.png)
4. Run the command "sudo systemctl start AssessorService"


## Configuration ##
		

### Property File Configuration ###
CIS-CAT Pro Assessor v4 Service includes two properties files located in the “config” folder where default options can be configured. Options relevant to CIS-CAT Pro v4 Service are defined below:

**assessor-service.properties**

| Property                         | Description                                   |
| -------------------------------- | --------------------------------------------- |
| produce.assessment.output.files  | By default, this feature is turned off and set to the recommended ‘false’ value. If set to ‘true’, every target system assessment will produce a detailed runtime log in the "logs" folder.  Although useful for debugging and troubleshooting, CIS recommends leaving this property set to 'false' as it may consume excessive disk space.
| ciscat.post.parameter.ccpd.token | CIS-CAT Pro Dashboard generated token. The same token can be used from existing CIS-CAT Pro Assessor v4 assessor-cli.properties file. See CIS-CAT Pro Dashboard documentation for more information on generating a token. |

**server.conf**

CIS-CAT Pro Assessor v4 Service includes a properties file used exclusively for setting properties utilized for configuring the embedded Web server. Use the information from the certificate generation process to set the property values below.


| Property                         | Description                                        |
| -------------------------------- | -------------------------------------------------- |
| server.http.port  | The listening port for Web service requests from CIS-CAT Pro Dashboard. You must ensure this port is open on the Assessor Service host machine, if you intend to use HTTP.  Default is set to 8080. HTTP is NOT recommended when CIS-CAT Pro Assessor v4 Service resides on a separate host than CIS-CAT Pro Dashboard Web server. If you will be using HTTPS, you can leave this property set to its default value.
| server.https.port | The listening port for Web service requests from CIS-CAT Pro Dashboard. You must ensure this port is open on the Assessor Service host machine, if you intend to use HTTPS.  Default is set to 443. If you do not intend to use HTTPS, you can leave this property set to its default value.
| server.ssl.keystore.location | Sets the full path and file name to the location of the keystore for HTTPS connections. If you do not intend to use HTTPS, use the **"cacerts"** truststore file that is included with Java to set this property.  This file is usually found in the **lib\security** folder of your Java installation.  For example, when running Assessor Service on a Microsoft Windows host, you would set this property to something like **C:\\\Program Files\\\Java\\\jre1.8.0_241\\\lib\\\security\\\cacerts**, depending on where you have Java installed.
| server.ssl.keystore.password | Sets the password of the keystore used for HTTPS connections. If you do not intend to use HTTPS, use "changeit" to set this property since this is the default password for the cacerts truststore.
|server.ssl.key.password| Sets the password of the key used for HTTPS connections.  If you do not intend to use HTTPS, you can leave this property set to its default value.
| server.ssl.certificate.alias | Sets the alias of the public certificate used for HTTPS connections. Set this property to the alias of the ssl certificate you will be using.  If you do not intend to use HTTPS, you can leave this property set to its default value. 
| server.ssl.ignore.certificate.warnings | Indicates if HTTPS requests sent to the CIS-CAT Pro Dashboard should ignore an SSL certificate warnings.  If you do not intend to use HTTPS, you can leave this property set to its default value. |

### Create HTTPS Certificate ###
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


### Configure CIS-CAT Pro Dashboard Property File ###
See the [CIS-CAT Pro Dashboard instructions](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#cis-cat-pro-assessor-v4-service-integration) for configuration instructions that enable features to orchestrate assessments from the Dashboard.

##Benchmark Coverage##
CIS-CAT Pro Assessor v4 Service supports all CIS benchmarks included with CIS-CAT Pro Assessor v4, except for those that require interactive values. Interactive Benchmarks can be reviewed here: [https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/). Support for tailored benchmarks will follow in future releases.


