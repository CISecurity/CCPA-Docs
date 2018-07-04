![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor Configuration Guide #

**NOTE: CIS-CAT Pro Assessor v4 is currently in BETA and this documentation will change as a result of ongoing testing and feedback.  Until the official release of CIS-CAT Pro Assessor v4, please consider this document fluid.**


## Introduction ##
Utilizing the CIS-CAT Pro Assessor CLI, users are capable of performing both host-based (local) assessments, as well as remote-based assessments.  In order to perform assessments of remote endpoints, certain configurations must be made.  The intent of this document is to serve as a guide for enabling systems for remote-based assessments using CIS-CAT Pro Assessor.

## Sessions ##
CIS-CAT Pro Assessor v4's remote assessment capability depends on the configuration of "sessions"; connection parameters used to create a secure connection to the remote endpoint.  A session configuration requires a number of entries, which will vary depending on the connection type.

### Connection Types ###
A number of different connection types exist to allow for maximum flexibility and coverage for the assessment of various endpoints, ranging from the local host to remote Windows, Unix, Linux, and Mac endpoints, as well as Cisco network devices.

| Type                   | Value      |   Description |
| -----------------------| ---------- | ------------- |
| Local                  | `local`    | Usage of a "local" session is for a host-based assessment, mimicing the functionality of CIS-CAT Pro v3.  Standalone or command-line applications (such as CIS-CAT Pro Assessor CLI) may use the local session to continue host-based assessments of benchmarks and/or OVAL definitions. |
| SSH (Unix, Linux, Mac) | `ssh`      | The "ssh" session type represents a connection to a remote Unix, Linux, or Mac endpoint, via SSH (obviously).  SSH connections can be established with a `username/password` or a `username/path to a private key file`.|
| Windows                | `windows`  | The "windows" session type represents a WinRM connection to a remote Microsoft Windows environment.  Both workstations and servers are supported with this connection type and can currently be established using `username/password` authentication.|
| Cisco IOS              | `ios`      | The "ios" session type handles the specific case for the assessment of Cisco IOS network devices.  Depending on the specific configuration when the "ios" session type is used, CIS-CAT Pro Assessor will either establish a SSH connection using `username/password` or `username/path to a private key` authentication, or will create a modified local session, collecting information from an exported configuration file.|
| Cisco ASA              | `asa`      | The "asa" session type handles the specific case for the assessment of Cisco ASA devices.  Depending on the specific configuration when the "asa" session type is used, CIS-CAT Pro Assessor will either establish a SSH connection using `username/password` or `username/path to a private key` authentication, or will create a modified local session, collecting information from an exported configuration file.|


### Configuration Properties ###
A number of configuration properties exist, and will vary based on the session type.

| Property   | Description |
| ---------- | ----------- |
| `type`     | The `type` property MUST be configured to one of the connection types specified above (`local`, `ssh`, `windows`, `ios`, or `asa`).|
| `host`     | The `host` property is required for any remote connection, and can be either the hostname or IP address (v4 or v6) of the endpoint to be assessed.  Examples include `1.2.3.4` or `CIS-CAT-TEST`. <br/><br/> The `host` property is not needed when assessing against exported network device configuration files.<br/><br/> The `host` property is not needed when the session type is `local`.|
| `port`     | The `port` property is required for any remote connection.  When using the `ssh` connection type, the default value for the `port` property would be `22`.  When using the `windows` connection type, the defaut WinRM ports are `5985` for HTTP and `5986` for HTTPS. <br/><br/> The `port` property is not needed when assessing against exported network device configuration files.<br/><br/> The `port` property is not needed when the session type is `local`.|
| `user`     | The `user` property represents an administrator-level username, used to log on to the remote endpoint.  This can be a domain user or a local administrator on the remote endpoint, or a privileged user when logging on to Cisco network devices.<br/><br/> The `user` property is not needed when assessing against exported network device configuration files.<br/><br/> The `user` property is not needed when the session type is `local`.|
| `cred`     | The `cred` property represents the credentials for the `user`, in order to log on to the remote endpoint.  Note that this is not encrypted, so users must take great care in safeguarding the sessions configuration file(s).  <br/><br/>**NOTE**: When executing CIS-CAT Pro Assessor CLI, if a given session's configuration specifies neither the `cred` nor the `identity` property, the user will be prompted to enter credentials manually.  This **will block** assessment against other configured sessions until credentials are entered. <br/><br/> The `cred` property is not needed when assessing against exported network device configuration files.<br/><br/> The `cred` property is not needed when the session type is `local`.|
| `identity` | The `identity` property represents the full path to a private key file used for authentication to a remote endpoint.<br/><br/>**NOTE**: When executing CIS-CAT Pro Assessor CLI, if a given session's configuration specifies neither the `cred` nor the `identity` property, the user will be prompted to enter credentials manually.  This **will block** assessment against other configured sessions until credentials are entered. <br/><br/> The `identity` property is not needed when assessing against exported network device configuration files.<br/><br/> The `identity` property is not needed when the session type is `local`.|
| `enable`   | The `enable` property is used only in network device sessions (`ios` or `asa`) and represents the credentials needed to enter "privileged EXEC" mode; required for obtaining the full output of the `show tech-support` command. <br/><br/> The `enable` property is not needed when assessing against exported network device configuration files.<br/><br/> The `enable` property is not needed when the session type is `local`.|
| `tech`     | The `tech` property is REQUIRED when assessing the exported configuration of a network device.  This property specifies the full path to the exported configuration file. <br/><br/> When assessing non-network device endpoints, or assessing a network devices' current running configuration via SSH, the `tech` property is unnecessary.<br/><br/> The `tech` property is not needed when the session type is `local`.|
| `tmp_path`| The `tmp_path` property allows users to configure the location of the temporary "ephemeral" directory on the target host.  This "ephemeral" directory is created upon connection to the target endpoint, hosts any scripts which may require executing during system characteristics collection, and is deleted upon the Assessor's completion and session disconnect.  If this property is left blank or not included, the Assessor will use the default "temp" folder as defined for the operating system, such as `/tmp` or `C:\Windows\Temp`.|

### Examples ###
The examples below provide insight into the creation of a `sessions.properties` file, which can then be consumed by CIS-CAT Pro Assessor CLI to provide connection configurations when assessing a particular benchmark.  By default, CIS-CAT Pro Assessor CLI will ALWAYS attempt to load a default configuration file located in the application's `config` folder, named `sessions.properties`.

For example, if CCPA is installed at `C:\CIS\Assessor-CLI`, a file named `C:\CIS\Assessor-CLI\config\sessions.properties` will be searched for and loaded (if found).  If no `sessions.properties` files are found or specified, a default `local` session will be used.

Configure a session for the local host, defining a custom "temp" folder:

    session.1.type=local
	# Note that specifying Windows directory paths require a double-backslash "\\" as the path separator
    session.1.tmp_path=C:\\Temp

Configure a remote Windows session using a username/password:

    session.2.type=windows
    session.2.host=123.255.198.9
    session.2.port=5986
    session.2.user=Administrator1
    session.2.cred=s3cr3t3r!

Configure a remote Windows session using a username, but requiring manual password entry:

    session.3.type=windows
    session.3.host=100.50.25.75
    session.3.port=5986
    session.3.user=Administrator1

Configure a remote Linux session using a username/password, defining a custom "temp" folder:

    session.4.type=ssh
    session.4.host=ubuntu-test.example.org
    session.4.port=22
    session.4.user=ubuntu
    session.4.cred=s3cr3t3r!
    session.4.tmp_path=/home/ubuntu

Configure a remote Linux session using a username/private key:

    session.5.type=ssh
    session.5.host=ubuntu-test.example.org
    session.5.port=22
    session.5.user=ubuntu
    session.5.identity=/home/ubuntu/cis/ubuntu-test.ppk

Configure a remote Cisco IOS session using a username/password:

    session.6.type=ios
    session.6.host=9.8.7.6
    session.6.port=22
    session.6.user=admin
    session.6.cred=s3cr3t3r!
    session.6.enable=3nab!3d

Configure a remote Cisco IOS session using a username/private key:

    session.7.type=ios
    session.7.host=9.8.7.6
    session.7.port=22
    session.7.user=admin
    # Note that specifying Windows directory paths require a double-backslash "\\" as the path separator
    session.7.identity=C:\\CIS\\cisco-ios.ppk
    session.7.enable=3nab!3d

Configure a Cisco IOS session pointing to an exported configuration file:

    session.8.type=ios
    # Note that specifying Windows directory paths require a double-backslash "\\" as the path separator
    session.8.tech=C:\\CIS\\TS\\tech-support-export.txt


## Microsoft Windows Endpoint Configuration ##
CIS-CAT Pro Assessor v4 utilizes the prevalent SMB protocol for file manipulation and uses WinRM for process execution.  Once connected to a remote Windows endpoint, CIS-CAT Pro Assessor establishes an "ephemeral" directory to host script required for the collection of system characteristics from the endpoint.  Once the collection/assessment has completed and the session disconnected, the "ephemeral" directory is removed from the endpoint.

CIS-CAT Pro Assessor v4 supports both basic authentication for local accounts and Kerberos authentication for domain accounts.  When authenticating with domain accounts, the new-style domain syntax, e.g. **`ciscatuser@example.org`** must be used, and **NOT** the old-style domain syntax, such as `DOMAIN\User`.

The Assessor will access the administrative shares on the remote host, which are only accessible for users that are part of the **Administrators** on the remote host.

### Security Considerations ###
The majority of CIS benchmarks for Microsoft Windows operating systems contain recommendations restricting WinRM usage.  The following table indicates those restrictions which will need to be relaxed in order to enable remote assessment in CIS-CAT Pro Assessor.

| Recommendation | CIS Benchmark Value | Relaxed Value |
|----------------|---------------------|---------------|
| 18.6.1: Ensure 'Apply UAC restrictions to local accounts on network logons' is set to 'Enabled'| Enabled | Disabled|
| 18.9.86.2.1: Ensure 'Allow Basic authentication' is set to 'Disabled'| Disabled | Enabled |

### WinRM Configuration ###
In order for CIS-CAT Pro Assessor to connect to a remote Windows host, a number of configuration steps on those hosts must happen.  The following sections will describe the configurations.

#### Windows Firewall Configuration ####
CIS-CAT Pro Assessor v4 uses both the SMB and WinRM protocols in order to enable file manipulation and process execution, respectively.  As such, to connect to the remote host using SMB, ensure the host is reachable on port `445`.  To enable connection to the remote host using WinRM over HTTPS, ensure the host is reachable on port `5986`.

Users can enable these firewall rules simply using PowerShell and the script provided with the CIS-CAT Pro Assessor v4 application bundle.  The bundle will contain a `setup` folder, in which will be locate the **`CISCAT_Pro_Assessor_v4_Firewall_SMB_WinRM.ps1`** script.  Execute this script in PowerShell to configure the Windows Firewall.

#### Enable WinRM ####
On the remote Windows host, open a Command Prompt using the "Run as Administrator" option.  Enter the following command to enable the default configuration for WinRM:

	winrm quickconfig

A confirmation prompt may be presented to the user.  If so, type `Y` and hit `Enter`.  Performing the `quickconfig` will start the Windows Remote Management service, configure an HTTP listener and create exceptions in the Windows Firewall for the WinRM service.

By default, basic authentication is disabled in WinRM.  Enable it if CIS-CAT Pro Assessor will be authenticating to the endpoint using a local account:

	winrm set winrm/config/service/Auth @{Basic="true"}

By default, Kerberos authentication is enabled in WinRM.  Disable it if CIS-CAT Pro Assessor will **NOT** be authenticating using domain accounts:

	winrm set winrm/config/service/Auth @{Kerberos="false"}

**NOTE**: Do not disable "Negotiate" authentication as the `winrm` command itself uses that to configure the WinRM subsystem.

Finally, configure WinRM to provide enough memory to the commands that are going to be executed, e.g. 1024 MB:

	winrm set winrm/config/winrs @{MaxMemoryPerShellMB="1024"}

#### Configure WinRM over HTTPS ####
In order for CIS-CAT Pro Assessor to access the remote Windows host using WinRM over HTTPS, an HTTPS WinRM Listener must be configured using the thumbprint of a certificate for that host.

Users can attempt to find an existing certificate thumbprint for the remote host using PowerShell.  In the following commands, assume `HOSTNAME` is the DNS name of the remote Windows host:

    PS C:\Windows\system32> Get-childItem cert:\LocalMachine\Root\ | Select-String -pattern HOSTNAME

If a certificate exists on the system, the PowerShell command will yield results similar to the following:

    [Subject]
       CN=HOSTNAME
    
     [Issuer]
       CN=HOSTNAME
    
     [Serial Number]
       527E7AF9142D96AD49A10469A264E766
    
     [Not Before]
       5/23/2011 10:23:33 AM
    
     [Not After]
       5/20/2021 10:23:33 AM
    
     [Thumbprint]
       5C36B638BC31F505EF7F693D9A60C01551DD486F

Once the certificate thumbprint is found, create the HTTPS WinRM listener for the remote host:

	winrm create winrm/config/Listener?Address=*+Transport=HTTPS @{Hostname="HOSTNAME"; CertificateThumbprint="THUMBPRINT"}

Where `HOSTNAME` is the DNS name of the remote host, such as `WINSERVER1`, and `THUMBPRINT` is the certificate thumbprint found in PowerShell, for example `5C36B638BC31F505EF7F693D9A60C01551DD486F`

If no results are returned, the user may create a self-signed certificate using PowerShell and a script provided with the CIS-CAT Pro Assessor v4 application bundle.  The bundle will contain a `setup` folder, in which will be located the **`CISCAT_Pro_Assessor_v4_SelfSignedCertificate.ps1`** script.  Execute this script in PowerShell to configure the self-signed certificate and create the WinRM HTTPS listener.

#### Disable UAC remote restrictions ####
To better protect those users who are members of the local Administrators group, Microsoft implemented UAC restrictions on the network. This mechanism helps prevent against "loopback" attacks. This mechanism also helps prevent local malicious software from running remotely with administrative rights.

When a user who is a member of the local administrators group on the target remote computer establishes a remote administrative connection by using the `net use * \\remotecomputer\Share$` command, for example, they will not connect as a full administrator. The user has no elevation potential on the remote computer, and the user cannot perform administrative tasks. If the user wants to administer the workstation with a Security Account Manager (SAM) account, the user must interactively log on to the computer that is to be administered with Remote Assistance or Remote Desktop, if these services are available.

To disable UAC remote restrictions, follow these steps: 

1. Click Start, click Run, type `regedit`, and then press `ENTER`.
2. Locate and then click the following registry subkey:

	`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`

3. If the `LocalAccountTokenFilterPolicy` registry entry does not exist, follow these steps: 
	1. On the Edit menu, point to `New`, and then click `DWORD Value`.
	2. Type `LocalAccountTokenFilterPolicy`, and then press `ENTER`.
4. Right-click `LocalAccountTokenFilterPolicy`, and then click `Modify`.
5. In the Value data box, type `1`, and then click `OK`.
6. Exit Registry Editor.

In Windows domain environments, this setting can be configured through Group Policy, however, the Group Policy Object is not a standard policy and must be downloaded and installed separately.  Generally, if an environment has installed the Microsoft Security Compliance Manager (SCM), the GPO is included there and can be exported.

Otherwise, the Group Policy Objects can be found either [here](http://blogs.technet.com/b/secguide/archive/2014/08/13/security-baselines-for-windows-8-1-windows-server-2012-r2-and-internet-explorer-11-final.aspx) or [here](https://blogs.technet.microsoft.com/secguide/2017/08/30/security-baseline-for-windows-10-creators-update-v1703-final/).


#### Domain Considerations ####
If users are planning on authenticating to remote Windows hosts using domain accounts, configuration is necessary both on the remote host, and on the "source" host (the machine hosting CIS-CAT Pro Assessor v4).

**Kerberos - Source Host**

Depending on the operating system of the source hose, create a file called `krb5.conf` (Unix) or `krb5.ini` (Windows) with at least the following content:

    [realms]
    EXAMPLE.ORG = {
    	kdc = KDC.EXAMPLE.ORG
    }

Replace the values with the name of your domain/realm and the hostname of your domain controller (multiple entries can be added to allow the source host to connect to multiple domains) and place the file in the default location for your operating system:

- Linux: `/etc/krb5.conf`
- Solaris: `/etc/krb5/krb5.conf`
- Windows: `C:\Windows\krb5.ini`

**Kerberos - Remote Host**

By default, the CIS-CAT Pro Assessor's connection to a remote Windows host will request access to a Kerberos service principal name of the form `WSMAN/HOST`.  This SPN should be configured automatically when configuring WinRM for the remote host (the "Enable WinRM" section above).

To verify the SPN has been created, list all the SPNs configured on the remote host:

	setspn -L HOSTNAME

If the `WSMAN/HOSTNAME` SPN is not listed, it must be configured.  From any host in the domain, invoke the `setspn` command:

	setspn -A WSMAN/ADDRESS HOSTNAME

Where `ADDRESS` is the address (DNS Name or IP Address) used to connect to the remote host, and `HOSTNAME` is the short Windows hostname of the remote host.

## Unix/Linux/OSX Endpoint Configuration ##
CIS-CAT Pro Assessor assesses remote Unix/Linux/OSX targets via SSH connections.  Ensure the target system can be accessed via SSH and that the user connecting to the remote target is either the `root` user or a user granted privileges to execute commands using `sudo`.

### Allowing Script Check Engine Environment Variables ###
When executing assessments against Unix/Linux/OSX platforms, many CIS benchmarks leverage the Script Check Engine (SCE) in order to quickly assess recommendations that would otherwise evaluate very slowly.  The Script Check Engine utilizes a number of environment variables, all prefaced with `XCCDF_` in order to pass variable values and provide Pass/Fail return codes.  When SSH'ing into a remote Unix/Linux/OSX platform, many systems restrict the SSH user's ability to set environment variable values.  In order to enable the creation of these variables, the target system must be configured to allow it.  The system's `/etc/ssh/sshd_config` file must be edited, adding the following line:

	AcceptEnv XCCDF_*

Once added, the system should be restarted in order for the configuration to take effect.

## Cisco Network Device Endpoint Configuration ##
CIS-CAT Pro Assessor v4 can assess either the current running configuration of a Cisco network device, or an exported configuration file.

### Connecting to a Device ###
CIS-CAT Pro Assessor assesses Cisco network device targets via SSH connections.  Ensure the target system can be accessed via SSH and that the user connecting to the remote target is a privileged user.  When connecting to Cisco devices, CIS-CAT Pro Assessor will be configured to enter "privileged EXEC" mode, so any user connecting to the Cisco device via SSH must be granted appropriate permission to do so.

### Exported Configuration File ###
CIS-CAT Pro Assessor can also assess an exported configuration file; the output of the `show tech-support` command.  The output from the `show tech-support` command is very long. To better manage this output, you can redirect the output to a file (for example, `show tech-support > *filename*` ) in the local writable storage file system or the remote file system.

You can use one of the following redirection methods:

	> filename —Redirects the output to a file.
	>> filename —Redirects the output to a file in append mode.

This example shows how to redirect the technical support information to a file:

	switch# show tech-support > bootflash:TechSupport.txt

Once the exported configuration file is available to CIS-CAT Pro Assessor, the assessment can be performed against it.  See the example above entitled "Configure a Cisco IOS session pointing to an exported configuration file" to configure the appropriate Assessor "session".

## Database Endpoint Configuration ##
Assessing database benchmarks in CIS-CAT Pro Assessor v4 uses the same JDBC connection mechanism as previous versions.  Database benchmarks will require a user to enter the JDBC connection string, or utilize the `ciscat.properties` file to set the appropriate value for assessment.

### Oracle Database ###
The JDBC string parameter is the connection string used to connect to and authenticate to the Oracle Database service and instance that CIS-CAT will assess.  The Oracle JDBC driver has the ability to connect to Oracle database instances using either the SID or Service Name.

When connecting to an Oracle database using the SID, the format of the JDBC connection string is:

	jdbc:oracle:thin:[username]/[password]@[hostname]:[port]:[SID]

For example:

	jdbc:oracle:thin:sys as sysdba/pa55w0rd!@servername:1521:ORCL

When connecting to an Oracle database using the Service Name, the format of the JDBC connection string is:

	jdbc:oracle:thin:[username]/[password]@//[hostname]:[port]/[service_name]

For example:

	jdbc:oracle:thin:sys as sysdba/pa55w0rd!@//servername:1521/SERVICE_NAME

The following table describes the components of the Oracle JDBC connection string.

| Property Name | Property Description |
|---------------|----------------------|
| username      | A valid username who can connect to the database instance.  This user should have sufficient privileges to `SELECT` from the various tables and views indicated in the specific Oracle benchmark, or be granted `SYSDBA` privileges. |
| password      | The credentials for the specified `username` to connect to the database instance. |
| hostname      | The name of the server (or it's IP address) hosting the database.|
| port          | The port number on which the database is listening.  By default, Oracle databases are configured to listen on port 1521.|
| SID           | The database SID.|
| Service Name  | The database Service Name.|


### Oracle MySQL Database ###
Oracle MySQL database support is implemented using the MariaDB JDBC driver.  The format for the MariaDB JDBC connection string for MySQL is:

	jdbc:mysql://<host>:<port>/<database>?<key1>=<value1>&<key2>=<value2>...

Consider a MySQL database instance with the following information:

| Property Name | Property Value |
|---------------|----------------------|
| Server Name   | CIS-SERVER |
| Database Name | TestDB |
| Database Port | 3306 |
| Username      | db_user |
| Credentials   | db_pass |

When configuring the JDBC connection string in CIS-CAT Pro Assessor, the above information would yield:

	jdbc:mysql://CIS-SERVER:3306/TestDB?user=db_user&password=db_pass

Notable optional parameters involve ensuring JDBC connections are made via SSL:

| Property Name          | Property Description |
|------------------------|----------------------|
| user                   | The database username. |
| password               | The credentials for the specified `username` to connect to the database instance. |
| useSSL                 | Force the usage of SSL on the connection. |
| trustServerCertificate | When using SSL, do *not* verify the server's certificate.|
| serverSslCert          | Server's certificate in DER form, or server's CA certificate. Can be used in one of 3 forms:<br/><br/> `serverSslCert=/path/to/cert.pem`:  full path to certificate <br/><br/> `serverSslCert =classpath:relative/cert.pem`:  relative to current classpath <br/><br/> or as verbatim DER-encoded certificate string, starting with<br/> `------BEGIN CERTIFICATE-----`|

**NOTES**

- The default port number for MySQL is 3306
- The full set of connection properties/optional URL parameters supported by MariaDB can be found at [https://mariadb.com/kb/en/mariadb/about-the-mariadb-java-client/](https://mariadb.com/kb/en/mariadb/about-the-mariadb-java-client/)


### Microsoft SQL Server ###
Microsoft SQL Server database support is implemented using the jTDS open source JDBC driver.  The jTDS driver provides support for SQL Server 6.5, 7, 2000, 2005, 2008, and 2012.

The format of the jTDS JDBC URL for MS SQL Server is:

	jdbc:jtds:sqlserver://<server>[:<port>][/<database>][;<property>=<value>]

Properties required for the database connection can be provided as `<property>=<value>` pairs, separated by a semi-colon `;`

Consider a Microsoft SQL Server database instance with the following information:

| Property Name                     | Property Value |
|-----------------------------------|----------------------|
| Server Name                       | CIS-SERVER |
| Database Name                     | TestDB |
| Database Port                     | 1433 |
| Windows Domain                    | WIN-DOMAIN |
| Windows Domain User/Password      | jsmith/qw3rty |
| SQL Server Database User/Password | db_user/db_pass |
| Instance Name                     | InstanceName |

#### Windows Authentication ####
Windows Authentication Mode allows a user to connect to a SQL Server instance through a Microsoft Windows user account.  This mode allows domain user account information to be supplied in order to establish a connection.  The following JDBC connection string would be valid for establishing a connection using the above example information:

	jdbc:jtds:sqlserver://CIS-SERVER:1433/TestDB;domain=WIN-DOMAIN;user=jsmith;password=qw3rty;instance=InstanceName

Windows Authentication Mode may also be used against databases running on machines not joined to a domain (standalone servers).  When authenticating with Microsoft Windows user accounts to non-domain joined servers, substitute in the computer name for the domain.  For example, if the name of the standalone server is `SQLSERVER`, the JDBC connection string would look as such:

	jdbc:jtds:sqlserver://CIS-SERVER:1433;DatabaseName=TestDB;domain=SQLSERVER;user=jsmith;password=qw3rty;instance=InstanceName

**NOTE**:  When connecting to a SQL Server using Windows Authentication, a common error message indicates that “the user is attempting to log in from an untrusted domain” (or similar message).  In order to resolve this issue, add the **`useNTLMv2=true`** property/value:

	jdbc:jtds:sqlserver://CIS-SERVER:1433;DatabaseName=TestDB;domain=SQLSERVER;user=jsmith;password=qw3rty;instance=InstanceName;useNTLMv2=true

#### SQL Server Authentication ####
SQL Server Authentication provides the ability for connections to a database instance to be made using trusted username and password information, allowing SQL Server to perform the authentication itself by checking to see if a SQL Server login account has been setup and if the password matches one previously recorded for that user.  The following JDBC URLs would be valid for establishing a connection using the above example information:

	jdbc:jtds:sqlserver://CIS-SERVER:1433/TestDB;user=db_user;password=db_pass;instance=InstanceName

or

	jdbc:jtds:sqlserver://CIS-SERVER:1433;DatabaseName=TestDB;user=jsmith;password=qw3rty;instance=InstanceName

**NOTES**:

- The default port number for MS SQL Server databases is `1433`.
- The full set of connection properties supported by jTDS can be found at [http://jtds.sourceforge.net/faq.html#urlFormat](http://jtds.sourceforge.net/faq.html#urlFormat).

## VMware ESXi Endpoint Configuration ##
Currently in development for support in CIS-CAT Pro Assessor v4.


## Extra configuration Options ##

	-sessions, --sessions <SESSIONS.PROPERTIES>
The `-sessions` option allows users to configure multiple endpoints for assessment of a benchmark.  The `sessions.properties` file configures CIS-CAT Pro Assessor for the assessment of remote endpoints by specifying remote hosts, ports, and credentials which the application will use for connection, collection and evaluation of benchmark recommendations and/or vulnerabilities.  See "Remote Assessment Capability" below for more information.

If no `sessions.properties` file exists or no connections are configured in the file, CIS-CAT Pro Assessor CLI will assess the local machine.


