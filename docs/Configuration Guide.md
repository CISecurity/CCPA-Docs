CIS-CAT Pro Assessor Configuration Guide
========================================

![](http://i.imgur.com/5yZfZi5.jpg)


Introduction
------------
Utilizing the CIS-CAT Pro Assessor CLI, users are capable of performing both host-based (local) assessments, as well as remote-based assessments.  In order to perform assessments of remote endpoints, certain configurations must be made.  The intent of this document is to serve as a guide for enabling systems for remote-based assessments using CIS-CAT Pro Assessor.

Sessions
--------
CIS-CAT Pro Assessor v4's remote assessment capability depends on the configuration of "sessions"; connection parameters used to create a secure connection to the remote endpoint.  A session configuration requires a number of entries, which will vary depending on the connection type.

### Connection Types ###
A number of different connection types exist to allow for maximum flexibility and coverage for the assessment of various endpoints, ranging from the local host to remote Windows, Unix, Linux, and Apple OSX endpoints, as well as Cisco network devices.

| Type                   | Value      |   Description |
| -----------------------| ---------- | ------------- |
| Local                  | `local`    | Usage of a "local" session is for a host-based assessment, mimicing the functionality of CIS-CAT Pro v3.  Standalone or command-line applications (such as CIS-CAT Pro Assessor CLI) may use the local session to continue host-based assessments of benchmarks and/or OVAL definitions. |
| SSH (Unix, Linux, Apple OSX) | `ssh`      | The "ssh" session type represents a connection to a remote Unix, Linux, or Apple OSX endpoint, via SSH (obviously).  SSH connections can be established a number of different ways, including `username/password`, `username/path to a private key file`, `username/private key file protected with a passphrase`, `username/private key file + credentials to use for sudo`.|
| Windows                | `windows`  | The "windows" session type represents a WinRM connection to a remote Microsoft Windows environment.  Both workstations and servers are supported with this connection type and can currently be established using `username/password` authentication.|
| Cisco IOS              | `ios`      | The "ios" session type handles the specific case for the assessment of Cisco IOS network devices.  Depending on the specific configuration when the "ios" session type is used, CIS-CAT Pro Assessor will either establish a SSH connection using `username/password` or `username/path to a private key` authentication, or will create a modified local session, collecting information from an exported configuration file.|



### Configuration Properties ###
A number of configuration properties exist, and will vary based on the session type.

| Property   | Description |
| ---------- | ----------- |
| `type`     | The `type` property MUST be configured to one of the connection types specified above (`local`, `ssh`, `windows`, or `ios`).|
| `host`     | The `host` property is required for any remote connection, and can be either the hostname or IP address (v4 or v6) of the endpoint to be assessed.  Examples include `1.2.3.4` or `CIS-CAT-TEST`. <br/><br/> The `host` property is not needed when assessing against exported network device configuration files.<br/><br/> The `host` property is not needed when the session type is `local`.|
| `port`     | The `port` property is required for any remote connection.  When using the `ssh` connection type, the default value for the `port` property would be `22`.  When using the `windows` connection type, the defaut WinRM ports are `5985` for HTTP and `5986` for HTTPS. <br/><br/> The `port` property is not needed when assessing against exported network device configuration files.<br/><br/> The `port` property is not needed when the session type is `local`.|
| `user`     | The `user` property represents an administrator-level username, used to log on to the remote endpoint.  This can be a domain user or a local administrator on the remote endpoint, or a privileged user when logging on to Cisco network devices.<br/><br/> The `user` property is not needed when assessing against exported network device configuration files.<br/><br/> The `user` property is not needed when the session type is `local`.|
| `cred`     | The `cred` property represents the credentials for the `user`, in order to log on to the remote endpoint.  Note that this is not encrypted, so users must take great care in safeguarding the sessions configuration file(s).  <br/><br/>**NOTE**: When executing CIS-CAT Pro Assessor CLI, if a given session's configuration specifies neither the `cred` nor the `identity` property, the user will be prompted to enter credentials manually.  This **will block** assessment against other configured sessions until credentials are entered. <br/><br/> The `cred` property is not needed when assessing against exported network device configuration files.<br/><br/> The `cred` property is not needed when the session type is `local`.|
| `identity` | The `identity` property represents the full path to a private key file used for authentication to a remote endpoint.<br/><br/>**NOTE**: When executing CIS-CAT Pro Assessor CLI, if a given session's configuration specifies neither the `cred` nor the `identity` property, the user will be prompted to enter credentials manually.  This **will block** assessment against other configured sessions until credentials are entered. <br/><br/> The `identity` property is not needed when assessing against exported network device configuration files.<br/><br/> The `identity` property is not needed when the session type is `local`.|
| `identityPassphrase` | The `identityPassphrase` property is optional and should be used in conjunction with the `identity` property, when that key is protected with a passphrase.|
| `enable`   | The `enable` property is used only in network device sessions (`ios`) and represents the credentials needed to enter "privileged EXEC" mode; required for obtaining the full output of the `show tech-support` command. <br/><br/> The `enable` property is not needed when assessing against exported network device configuration files.<br/><br/> The `enable` property is not needed when the session type is `local`.|
| `tech`     | The `tech` property is REQUIRED when assessing the exported configuration of a network device.  This property specifies the full path to the exported configuration file. <br/><br/> When assessing non-network device endpoints, or assessing a network devices' current running configuration via SSH, the `tech` property is unnecessary.<br/><br/> The `tech` property is not needed when the session type is `local`.|
| `tmp`| The `tmp` property allows users to configure the location of the temporary "ephemeral" directory on the target host.  The "ephemeral" directory is named `ccpa-temp-TIMESTAMP` and is created as a sub-folder of the directory specified in this setting.  For example, if `tmp` is specified as `C:\Temp`, the "ephemeral" directory will be created at `C:\Temp\ccpa-temp-TIMESTAMP`.  **NOTE**: When specifying a value for `tmp`, this directory MUST ALREADY EXIST on the target endpoint.  In the above example, if the `C:\Temp` folder does not exist, the connection from CIS-CAT Pro Assessor v4 will not succeed.  If this property is left blank or not included, the Assessor will use the default "temp" folder as defined for the operating system, such as `/tmp` or `C:\Windows\Temp`.|

### Examples ###
The examples below provide insight into the creation of a `sessions.properties` file, which can then be consumed by CIS-CAT Pro Assessor CLI to provide connection configurations when assessing a particular benchmark.  By default, CIS-CAT Pro Assessor CLI will ALWAYS attempt to load a default configuration file located in the application's `config` folder, named `sessions.properties`.

Microsoft Windows install
-----------------------------------------

For example, if CCPA is installed at `C:\CIS\Assessor-CLI`, a file named `C:\CIS\Assessor-CLI\config\sessions.properties` will be searched for and loaded (if found).  If no `sessions.properties` files are found or specified, a default `local` session will be used.

Configure a session for the local Microsoft Windows host, defining a custom "temp" folder:

    session.1.type=local
	# Note that specifying Windows directory paths require a double-backslash "\\" as the path separator
    session.1.tmp=C:\\Temp

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

Configure a remote Cisco IOS session using a username/password:

    session.4.type=ios
    session.4.host=9.8.7.6
    session.4.port=22
    session.4.user=admin
    session.4.cred=s3cr3t3r!
    session.4.enable=3nab!3d

Configure a remote Cisco IOS session using a username/private key:

    session.5.type=ios
    session.5.host=9.8.7.6
    session.5.port=22
    session.5.user=admin
    # Note that specifying Windows directory paths require a double-backslash "\\" as the path separator
    session.5.identity=C:\\CIS\\cisco-ios.ppk
    session.5.enable=3nab!3d

Configure a Cisco IOS session pointing to an exported configuration file:

    session.6.type=local

Linux install
------------------------

Configure a remote Linux session using a username/private key:

    session.7.type=ssh
    session.7.host=ubuntu-test.example.org
    session.7.port=22
    session.7.user=ec2-user
    session.7.identity=/home/myuser/cis/pkey.pem

MacOS install
--------------------------

Configure a remote Linux session using a username/private key:

    session.8.type=ssh
    session.8.host=ubuntu-test.example.org
    session.8.port=22
    session.8.user=ec2-user
    session.8.identity=/Users/myuser/cis/pkey.pem


Microsoft Windows Endpoint Configuration
----------------------------------------
CIS-CAT Pro Assessor v4 utilizes the SMB protocol for file manipulation and uses WinRM for process execution.  Once connected to a remote Windows endpoint, CIS-CAT Pro Assessor establishes an "ephemeral" directory to host scripts required for the collection of system characteristics from the endpoint.  Once the collection/assessment has completed and the session disconnected, the "ephemeral" directory is removed from the endpoint.

CIS-CAT Pro Assessor v4 supports authentication to remote Windows endpoints using either local or domain accounts.  When authenticating with domain accounts, the new-style domain syntax, e.g. **`ciscatuser@example.org`** must be used, and **NOT** the old-style domain syntax, such as `DOMAIN\User`.

The Assessor accesses the administrative shares on the remote host, which are only accessible for users that are part of the **Administrators** group on that host, or are configured as domain administrators.

When configuring WinRM for an environment, members must consider the following:

- **Will the configuration be done manually or through group policy?**
- **Will the Assessor access endpoints using WinRM over HTTP or HTTPS?** (see [Security Considerations](#security-considerations))
- **Will the Assessor authenticate to remote endpoints using a local administrator account or domain account?** (see [Security Considerations](#security-considerations))

### <a name="security-considerations"></a>Security Considerations ###
The answers to two of the above questions have security implications:

- If the Assessor will access remote endpoints using **WinRM over HTTP**, each endpoint must be configured to "Allow Unencrypted Traffic";
- If the Assessor will authenticate to remote endpoints using a **local administrator account**, each endpoint must disable the "Apply UAC restrictions to local accounts on network logons" configuration.

The majority of CIS benchmarks for Microsoft Windows operating systems contain recommendations that affect enabling remote assessment in CIS-CAT Pro.  If users plan to utilize remote assessment in their environment for Microsoft Windows operating systems, we recommend considering the risks of making deviations from the recommended CIS Benchmark setting.  Each notation below applies to the Level 1 Profile.

Please note the actual text of each benchmark recommendation may vary from the text noted in the table. 

| Usage | Recommendation | CIS Benchmark Value | Relaxed Value |
|-------|----------------|---------------------|---------------|
| WinRM over HTTP | Ensure 'Allow unencrypted traffic' is set to 'Disabled' | Disabled | Enabled |
| Authenticating with local administrator account | Ensure 'Apply UAC restrictions to local accounts on network logons' is set to 'Enabled'| Enabled | Disabled|

Each of these configurations represents a deviation from the CIS benchmark recommendations.

If a member organization has accepted the risk of remote configuration assessment and system values have been set to enable a remote connection, the assessment report will show a failure for the deviated settings. The failed recommendations may be handled in the CIS-CAT Pro Dashboard as exceptions with organization-provided rationale.

Because of these recommendations and potential for deviation, CIS recommends configuring WinRM over HTTPS and utilizing domain accounts when performing remote assessments.

CIS Benchmark Level 2 profiles are designed toward host-based assessments.  If selecting to remotely assess endpoints, an organization may choose to adopt Level 1 policies or tailor Level 2 policies as needed to enable remote scanning.

Finally, note that the CIS Microsoft Windows Benchmarks are written assuming Active Directory domain-joined systems using Group Policy, and not necessarily standalone/workgroup systems.  Adjustments/tailoring to some recommendations will be needed to maintain functionality when implementing CIS Benchmark recommendations on standalone systems.

### An Example Flowchart ###
The following flowchart outlines the decision-making process when configuring and environment for remote assessment using CIS-CAT Pro Assessor v4:

![](https://i.imgur.com/ye16W1v.png)

### Windows Firewall Configuration ###
CIS-CAT Pro Assessor v4 uses both the SMB and WinRM protocols in order to enable file manipulation and process execution, respectively.  As such, to connect to the remote host using SMB, ensure the host is reachable on port `445`.  To enable connection to the remote host using WinRM, ensure the host is reachable on either port `5985` (for WinRM over HTTP) or port `5986` (for WinRM over HTTPS).

Users can enable these firewall rules simply using PowerShell and the script provided with the CIS-CAT Pro Assessor v4 application bundle.  The bundle will contain a `setup` folder, in which will be locate the **`CISCAT_Pro_Assessor_v4_Firewall_SMB_WinRM.ps1`** script.  Execute this script in PowerShell to configure the Windows Firewall.

#### Configure WinRM over HTTPS ####
In order for CIS-CAT Pro Assessor to access the remote Windows host using WinRM over HTTPS, an HTTPS WinRM Listener must be configured using the thumbprint of a certificate for that host.

Users can attempt to find an existing certificate thumbprint for the remote host using PowerShell.  In the following commands, assume `HOSTNAME` is the DNS name of the remote Windows host:

    PS C:\Windows\system32> Get-childItem cert:\LocalMachine\My\ | Select-String -pattern HOSTNAME

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

If a valid certificate is found, a couple of options are available depending on the Windows version being configured.  For Windows Server 2012 and higher, HTTPS listeners may be created without needing to know the hostname or thumbprint.  Therefore, if the certificate is found, users can issue the following `winrm` command to configure the HTTPS listener:

	winrm quickconfig -transport:https -force

Alternatively, users can manually create the HTTPS WinRM listener as follows:

	winrm create winrm/config/Listener?Address=*+Transport=HTTPS @{Hostname="HOSTNAME"; CertificateThumbprint="THUMBPRINT"}

Where `HOSTNAME` is either the DNS name or FQDN of the remote host, such as `WINSERVER1` or `winserver1.domain.com`, respectively, and `THUMBPRINT` is the certificate thumbprint found in PowerShell, for example `5C36B638BC31F505EF7F693D9A60C01551DD486F`

If no results are returned, members may create a self-signed certificate using PowerShell and a script provided with the CIS-CAT Pro Assessor v4 application bundle.  The bundle will contain a `setup` folder, in which will be located the **`CISCAT_Pro_Assessor_v4_SelfSignedCertificate.ps1`** script.  Execute this script in PowerShell to configure the self-signed certificate and create the WinRM HTTPS listener.

### WinRM Configuration ###
In order for CIS-CAT Pro Assessor to connect to a remote Windows host, a number of configurations must be applied to those hosts.  This configuration can be applied either manually or through Group Policy.

#### <a name="gpo"></a>Group Policy Configuration ####
The WinRM service can be configured using Group Policy in two ways.  In domain environments, policies are maintained on the Domain Controller's Group Policy Management Console (GPMC).  Group Policy administrators can access the GPMC by clicking the Start menu and typing "Group Policy Management".  Once displayed in the available applications menu, right-click and select "Run as Administrator".  Once opened, the member should first create a new Group Policy Object, followed by right-clicking on the GPO and selecting "Edit".  In standalone (non-domain) environments, local administrators can edit the endpoint's Local Group Policy Object in a similar fashion.  To start the Local Group Policy editor, click the Start menu and type “gpedit.msc”.  Right-click and run it as an Administrator.  Alternatively, you can add the local Group Policy Object Editor to the Microsoft Management Console as a snap-in component:


1. Open the Start menu and enter **mmc**.  Right-click and run this application as an Administrator.
2. Select **File** and **Add/Remove Snap-ins**.
3. Under **Available Snap-ins**, select **Group Policy Object Editor** and click the **Add >** button.
4. In the wizard, make sure it’s choosing “Local Computer” and click **Finish**.
5. Click **OK**.

Once the Group Policy Object has been opened for editing, navigate to 


    Computer Configuration\Policies\Administrative Templates\Windows Components\Windows Remote Management (WinRM)\WinRM Service

Configure the following settings:

- **Allow remote server management through WinRM**:  Set to `Enabled`
	- This policy setting allows you to manage whether the Windows Remote Management (WinRM) service automatically listens on the network for requests. 
	- **NOTE**: Options exist for this setting.  Consult the descriptions in this group policy setting to configure any IPv4 or IPv6 filters in order to restrict which IP addresses are listened for.  Members could use an asterisk (*) to indicate that the service listens on all available IP addresses on the computer.
- **Allow unencrypted traffic**: Set to `Enabled`
	- **NOTE** This configuration is only required when using *WinRM over HTTP*.  See the [Security Considerations](#security-considerations) above for more information.  This setting is **NOT REQUIRED** when using *WinRM over HTTPS*.

If the Assessor will authenticate to remote endpoints using a **local administrator account** (See the [Security Considerations](#security-considerations) above for more information), navigate to:

    Computer Configuration\Policies\Administrative Templates\SCM: Pass the Hash Mitigations

If this group policy setting is not available, it may need to be downloaded and imported into the GPMC.  The administrative template (ADMX) files can be downloaded from either [here](http://blogs.technet.com/b/secguide/archive/2014/08/13/security-baselines-for-windows-8-1-windows-server-2012-r2-and-internet-explorer-11-final.aspx) or [here](https://blogs.technet.microsoft.com/secguide/2017/08/30/security-baseline-for-windows-10-creators-update-v1703-final/).

Once downloaded and made available in the GPMC, configure the following:

- **Apply UAC restrictions to local accounts on network logons**:  Set to `Disabled`
	- This setting controls whether local accounts can be used for remote administration via network logon (e.g., NET USE, connecting to C$, etc.). 
	- Configuring this setting to `Disabled` allows local accounts to have full administrative rights when authenticating via network logon, by configuring the `LocalAccountTokenFilterPolicy` registry value to 1.
	- Local accounts are at high risk for credential theft when the same account and password is configured on multiple systems.  Again, see the Security Considerations above to determine if local accounts are necessary to perform remote assessment with CIS-CAT Pro Assessor.

#### Manual Configuration ####
Configuring WinRM manually is not a complicated task, but does involve a number of commands on each endpoint that will be assessed remotely.  CIS recommends configuring endpoints via Group Policy in a domain environment, but manual configuration can be useful for testing environments.

##### Enable WinRM #####
On the remote Windows host, open a Command Prompt using the "Run as Administrator" option.  Enter the following command to enable the default configuration for WinRM:

	winrm quickconfig

A confirmation prompt may be presented to the user.  If so, type `Y` and hit `Enter`.  Performing the `quickconfig` will start the Windows Remote Management service, configure an HTTP listener and create exceptions in the Windows Firewall for the WinRM service.

If users intend to connect to remote endpoints using WinRM over HTTP (and not HTTPS), then WinRM must be configured to "Allow unencrypted traffic":

	winrm set winrm/config/service @{AllowUnencrypted="true"}

**NOTE** This configuration is only required when using *WinRM over HTTP*.  See the Security Considerations above for more information.  This setting is **NOT REQUIRED** when using *WinRM over HTTPS*.

##### Disable UAC remote restrictions #####
To better protect those users who are members of the local Administrators group, Microsoft implemented UAC restrictions on the network. This mechanism helps prevent against "loopback" attacks. This mechanism also helps prevent local malicious software from running remotely with administrative rights.

When a user who is a member of the local administrators group on the target remote computer establishes a remote administrative connection by using the `net use * \\remotecomputer\Share$` command, for example, they will not connect as a full administrator. The user has no elevation potential on the remote computer, and the user cannot perform administrative tasks. If the user wants to administer the workstation with a Security Account Manager (SAM) account, the user must interactively log on to the computer that is to be administered with Remote Assistance or Remote Desktop, if these services are available.

To disable UAC remote restrictions, follow these steps: 

- Click Start, click Run, type **regedit**, and then press **ENTER**.
- Locate and then click the following registry subkey:

	`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`
- If the `LocalAccountTokenFilterPolicy` registry entry does not exist, follow these steps: 
	- On the Edit menu, point to **New**, and then click **DWORD Value**.
	- Type **LocalAccountTokenFilterPolicy**, and then press **ENTER**.
- Right-click **LocalAccountTokenFilterPolicy**, and then click **Modify**.
- In the Value data box, type **1**, and then click **OK**.
- Exit Registry Editor.

In Windows domain environments, this setting can be configured through [Group Policy](#gpo), however, the Group Policy Object is not a standard policy and must be downloaded and installed separately.  Generally, if an environment has installed the Microsoft Security Compliance Manager (SCM), the GPO is included there and can be exported.

Otherwise, the Group Policy Objects can be found either [here](http://blogs.technet.com/b/secguide/archive/2014/08/13/security-baselines-for-windows-8-1-windows-server-2012-r2-and-internet-explorer-11-final.aspx) or [here](https://blogs.technet.microsoft.com/secguide/2017/08/30/security-baseline-for-windows-10-creators-update-v1703-final/).


Unix/Linux/OSX Endpoint Configuration
-------------------------------------
CIS-CAT Pro Assessor assesses remote Unix/Linux/OSX targets via SSH connections.  Ensure the target system can be accessed via SSH and that the user connecting to the remote target is either the `root` user or a user granted privileges to execute commands using `sudo`.

### A Note on the `/tmp` Partition ###
By default, CIS-CAT Pro Assessor v4 will attempt to create the "ephemeral" directory in the default temporary directory based on the operating system to which the Assessor is connecting.  For many Unix/Linux systems, this temporary directory is `/tmp`.  However, recommendations in many CIS Unix/Linux benchmarks suggest mounting the `/tmp` partition with the `noexec` option.  Mounting the partition with `noexec` disallows the execution of scripts from that partition, even if the `+x` permissions are enabled.  When CIS-CAT Pro Assessor v4 then uses the default `/tmp` folder to create the "ephemeral" directory, none of the application's scripts can be executed, due to the `noexec` mount option.

It is *highly recommended* that, when the `/tmp` partition is mounted with the `noexec` option, that users configure the `sessions.properties` or `assessor-config.xml` files to customize the `tmp` setting to an existing directory on the target endpoint which will allow for script execution.  Not doing so will result in numerous incorrect assessment results.

Cisco Network Device Endpoint Configuration
-------------------------------------------
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

Database Endpoint Configuration
-------------------------------
Assessing database benchmarks in CIS-CAT Pro Assessor v4 uses the same JDBC connection mechanism as previous versions.  Database benchmarks will require a user to enter the JDBC connection string, or utilize the `assessor-cli.properties` file to set the appropriate value for assessment.

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
| password               | The credentials for the specified `user` to connect to the database instance. |
| useSSL                 | Force the usage of SSL on the connection. |
| trustServerCertificate | When using SSL, do *not* verify the server's certificate.|
| serverSslCert          | Server's certificate in DER form, or server's CA certificate. Can be used in one of 3 forms:<br/><br/> `serverSslCert=/path/to/cert.pem`:  full path to certificate <br/><br/> `serverSslCert =classpath:relative/cert.pem`:  relative to current classpath <br/><br/> or as verbatim DER-encoded certificate string, starting with<br/> `------BEGIN CERTIFICATE-----`|

**NOTES**

- The default port number for MySQL is 3306
- The full set of connection properties/optional URL parameters supported by MariaDB can be found at [https://mariadb.com/kb/en/mariadb/about-the-mariadb-java-client/](https://mariadb.com/kb/en/mariadb/about-the-mariadb-java-client/)

### PostgreSQL Database ###
CIS-CAT Pro Assessor has implemented support for assessments against PostgreSQL database instances using the PostgreSQL JDBC driver.  The format for the PostgreSQL JDBC connection string is:

	jdbc:postgresql://<host>:<port>/<database>?<key1>=<value1>&<key2>=<value2>...

Consider a PostgreSQL database instance with the following information:

| Property Name | Property Value |
|---------------|----------------------|
| Server Name   | CIS-POSTGRESQL |
| Database Name | PostgreSQL-DB |
| Database Port | 5432 (the default) |
| Username      | db_user |
| Credentials   | db_pass |

When configuring the JDBC connection string in CIS-CAT Pro Assessor, the above information would yield:

	jdbc:postgresql://CIS-POSTGRESQL:5432/PostgreSQL-DB?user=db_user&password=db_pass

If CIS-CAT Pro Assessor is connecting to PostgreSQL on the default port (5432), it can be omitted from the connection string:

	jdbc:postgresql://CIS-POSTGRESQL/PostgreSQL-DB?user=db_user&password=db_pass

Notable optional parameters involve ensuring JDBC connections are made via SSL:

| Property Name          | Property Description |
|------------------------|----------------------|
| user                   | The database username. |
| password               | The credentials for the specified `user` to connect to the database instance. |
| ssl                 | A boolean value (`true` or `false`), to force the usage of SSL on the connection. |

For example, in order to force the database connection to require SSL, the connection string would look like:

	jdbc:postgresql://CIS-POSTGRESQL/PostgreSQL-DB?user=db_user&password=db_pass&ssl=true


**NOTES**

- The default port number for PostgreSQL is 5432
- The full set of connection properties/optional URL parameters supported by PostgreSQL can be found at [https://jdbc.postgresql.org/documentation/head/connect.html](https://jdbc.postgresql.org/documentation/head/connect.html)

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

VMware ESXi Endpoint Configuration
----------------------------------
Currently in development for support in CIS-CAT Pro Assessor v4.


Extra configuration Options
---------------------------

	-sessions, --sessions <SESSIONS.PROPERTIES>
The `-sessions` option allows users to configure multiple endpoints for assessment of a benchmark.  The `sessions.properties` file configures CIS-CAT Pro Assessor for the assessment of remote endpoints by specifying remote hosts, ports, and credentials which the application will use for connection, collection and evaluation of benchmark recommendations and/or vulnerabilities.  See "Remote Assessment Capability" below for more information.

If no `sessions.properties` file exists or no connections are configured in the file, CIS-CAT Pro Assessor CLI will assess the local machine.

<a name="assessMultipleWindowsTargets"></a>
## Assessing Multiple Windows Targets ##
It is possible to assess a population of Microsoft Windows targets in an automated manner without installing CIS-CAT or the JRE on each target. The following diagram depicts this deployment pattern:

![](https://i.imgur.com/gGUgx7K.png)

### CIS Host Server ###
The *CIS Host Server* is where the CIS-CAT bundle, Java Runtime Environment, and Reports are placed. Targets within the Workstations Group will access these resources to perform a self-assessment using CIS-CAT.

### Workstations Group ###
The *Workstations Group* represents a population of Microsoft Windows targets to be assessed with CIS-CAT. The Domain Administrator will create Group Policy that causes devices in this group to invoke CIS-CAT via a Scheduled Task.  In order to maintain a secure configuration of the CIS Host Server, authenticated users should only be allowed to execute the “cis-cat-centralized.bat” and "cis-cat-centralized-ccpd.bat" files.

### Prerequisites ###
1. All targets must be joined to an Active Directory Domain
2. All targets must have read access to the *CIS-CAT Share* hosted off of the *CIS Host Server*

### Setup ###
Perform the following steps to cause the *Workstations Group* to execute the CIS-CAT instance on the *CIS Host Server*.

#### Create CIS Share on the CIS Hosting Server ####
1. Create a shared folder on the *CIS Host Server* named **CIS**. Share permissions on the CIS folder should allow the Authenticated Users group the ability to both **Read** and **Change** information in the folder. To configure the permissions on the CIS share, right-click on the CIS folder and select “Properties”. Click on the “Sharing” tab, and select “Advanced Sharing”:

![](https://i.imgur.com/XvCEvEJ.png)

From the “Advanced Sharing” popup, select “Permissions”:

![](https://i.imgur.com/Md8TqnE.png)

On the “Permissions” popup, grant **Change** and **Read** to the Authenticated Users group:

![](https://i.imgur.com/KiAmbP0.png)

2. Unzip the CIS-CAT bundle within the **CIS** folder on the *CIS Host Server* and move the Assessor-CLI folder to the root of the **CIS** folder.
3. Create the following directories beneath the CIS folder on the *CIS Host Server*:
	- Java
	- Java64
	- Reports 
4. To copy the java runtime (JRE) to the CIS folder do the following:
	- Browse to the location where Java is installed, by default Java is located at “%ProgramFiles%\Java”.
	- Copy the 32-bit JRE that applies to the targets you will be evaluating, such as jre1.8.0_201, to the Java folder you created in step 3.
	- Copy the 64-bit JRE that applies to the targets you will be evaluating, such as jre1.8.0_201, to the Java64 folder you created in step 3.
5. Move the Assessor-CLI\misc\Windows\cis-cat-centralized.bat file or the Assessor-CLI\misc\Windows\cis-cat-centralized-ccpd.bat file to the root of the CIS folder, depending on whether you want to write the assessment reports to the *CIS Host Server* or configure the centralized script to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD).
6. Share the **CIS** folder as CIS.

The resulting directory structure should be as follows:

	- CIS\Assessor-CLI
	- CIS\Assessor-CLI\benchmarks
	- CIS\Assessor-CLI\config
	- CIS\Assessor-CLI\lib
	- CIS\Assessor-CLI\licenses
	- CIS\Assessor-CLI\misc
	- CIS\Assessor-CLI\reports
	- CIS\Assessor-CLI\sce
	- CIS\Assessor-CLI\scripts
	- CIS\Assessor-CLI\setup
	- CIS\Assessor-CLI\Assessor-CLI.jar
	- CIS\cis-cat-centralized.bat or CIS\cis-cat-centralized-ccpd.bat
	- CIS\Java
	- CIS\Java64
	- CIS\Reports

#### Security Considerations ####
The CIS\Reports folder will contain reports that detail configuration related vulnerabilities for each system evaluated by CIS-CAT. As such, “Authenticated Users” should **only** be granted “Write” and “List Folder Contents” access to the contents of this folder, and read access to the CIS\Reports folder should be restricted to only those personnel who are necessary to the appropriate functioning of the *CIS Host Server*:

![](https://i.imgur.com/wCMWpV1.png)

Permissions which should be applied within the **CIS** folder on the *CIS Host Server*:

|File or Folder                   |Permissions                                        |
|---------------------------------|---------------------------------------------------|
|CIS                              |Permissions on the shared folder                   |
|CIS\cis-cat-centralized.bat **or** CIS\cis-cat-centralized-ccpd.bat |**Execute** to “Authenticated Users” |
|CIS\Assessor-CLI (folder) |**List Folder Contents**, **Read**, and **Read & Execute** to "Authenticated Users" |
|CIS\Java (folder) |**Read** and **Read & Execute** to “Authenticated Users” |
|CIS\Java64 (folder) |**Read** and **Read & Execute** to “Authenticated Users” |
|CIS\Reports (folder) |**List Folder Contents** and **Write** to “Authenticated Users” |

Additionally, Write, Modify, Read and Execute permissions on the above resources should be limited to only those users necessary to the appropriate functioning of the *CIS Host Server*.

#### Update cis-cat-centralized.bat ####
Once the **CIS** folder is setup on the *CIS Hosting Server*, a few modifications must be made to either `cis-cat-centralized.bat` or `cis-cat-centralized-ccpd.bat`. If you want to write the assessment reports to the *CIS Host Server*, utilize the `cis-cat-centralized.bat` script and modify it as directed in this section.  If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD), skip this section and go to the **"Update cis-cat-centralized-ccpd.bat"** section, instead. 

	SET NetworkShare=\\NETWORK_SHARE\CIS
Replace `NETWORK_SHARE` with the fully qualified domain name or IP address of the CIS-CAT Host Server.

	SET JavaPath=Java\jre
	SET JavaPath64=Java64\jre
Note that the 32-bit and 64-bit JRE paths are those installed in step 4 under the **Create CIS Share on the CIS Hosting Server** section above.

	SET JavaMaxMemoryMB=768
Indicate the maximum amount of memory CIS-CAT will allocate for execution.  The default is 768 MB.  When executing with 32-bit versions of the JRE, this value can be set to a maximum of 2048 MB.  64-bit JRE’s may allocate as much memory as is required, limited by the available memory of machines invoking CIS-CAT.

	SET CisCatPath=Assessor-CLI
Set the CisCatPath value to the location, relative to the network share, of the installed version of CIS-CAT.  For example, the value above indicates the path to CIS-CAT is `\\NETWORK_SHARE\CIS\Assessor-CLI`.

	SET ReportsPath=Reports
Set the ReportsPath value to the location, relative to the network share, of the folder to which CIS-CAT reports are written.  For example, the value above indicates `\\NETWORK_SHARE\CIS\Reports` as the location to which reports are written.

	SET CISCAT_OPTS=-html -txt -csv
Finally, set the various reporting options to be used when launching CIS-CAT.

* `-html` indicates generation of the CIS-CAT XML report.
* `-txt` indicates generation of the CIS-CAT Text report.
* `-csv` indicates generation of the CIS-CAT CSV report.
* `-narf` indicates that CIS-CAT should NOT generate an Asset Reporting Format (ARF) report.

**Configuration Note:**  The “cis-cat-centralized.bat” script sets local environment variables denoting file system paths and folder names.  CIS recommends, for simplicity, that these paths do not contain spaces, as without modification to the script, spaces in paths can cause unexpected behavior.

Near line 780 of the “cis-cat-centralized.bat” script, the following code section illustrates the configuration of the CIS-CAT command-line for execution.

	Put all the options together and form the CIS-CAT command-line
	
	SET FULL_CISCAT_CMD=%mJavaPath%\bin\java.exe -Xmx%JavaMaxMemoryMB%M -jar %mCisCatPath%\Assessor-CLI.jar %CISCAT_OPTS% -b %mCisCatPath%\benchmarks\%Benchmark%
	
	ECHO	  Benchmark:	%Benchmark%
	ECHO	 Profile(s):	%Profiles%
	ECHO.
	ECHO Starting Assessment(s)...
	FOR %%P IN (%Profiles%) DO (
		ECHO  + %FULL_CISCAT_CMD% -p "%%P" -r "%mReportsPath%"
		ECHO  + Running Profile %%P...
		ECHO.
		ECHO [[ CIS-CAT ASSESSMENT START ]]
		IF %DEBUG%==1 ECHO CMDLINE = %FULL_CISCAT_CMD% -p "%%P" -r "%mReportsPath%" >> %DebugLogFile%
		%FULL_CISCAT_CMD% -p "%%P" -r "%mReportsPath%" 
		ECHO [[  CIS-CAT OUTPUT END  ]]
		ECHO.
	)

When spaces are included in any path names for environment variables, they must be surrounded with quotes to enable the full path to be discovered, for example:

	SET FULL_CISCAT_CMD=”%mJavaPath%\bin\java.exe” -Xmx%JavaMaxMemoryMB%M -jar “%mCisCatPath%\CISCAT.jar” -a 
	-s %CISCAT_OPTS% -b “%mCisCatPath%\benchmarks\%Benchmark%”

#### Update cis-cat-centralized-ccpd.bat ####
If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD) you have already setup, you must use the `cis-cat-centralized-ccpd.bat` file instead of the `cis-cat-centralized.bat` file.  Modify the `cis-cat-centralized-ccpd.bat` file as follows: 

	SET NetworkShare=\\CisHostServer\CIS
Replace `CisHostServer` with the fully qualified domain name or IP address of the CIS-CAT Host Server.

	SET JavaPath=Java\jre
	SET JavaPath64=Java64\jre
Note that the 32-bit and 64-bit JRE paths are those installed in step 4 under the **Create CIS Share on the CIS Hosting Server** section above.

	SET JavaMaxMemoryMB=768
Indicate the maximum amount of memory CIS-CAT will allocate for execution.  The default is 768 MB.  When executing with 32-bit versions of the JRE, this value can be set to a maximum of 2048 MB.  64-bit JRE’s may allocate as much memory as is required, limited by the available memory of machines invoking CIS-CAT.

	SET CisCatPath=Assessor-CLI
Set the CisCatPath value to the location, relative to the network share, of the installed version of CIS-CAT.  For example, the value above indicates the path to CIS-CAT is `\\NETWORK_SHARE\CIS\Assessor-CLI`.

	SET CCPDUrl=http://[YOUR-SERVER]/CCPD/api/reports/upload
Set the URL for the CIS-CAT Pro Dashboard API to which CIS-CAT assessment reports will be uploaded.  The resource for CIS-CAT Pro Dashboard upload is **ALWAYS** mapped to the `/api/reports/upload` location, so the path to the application is all that should be modified here.  For example: http://applications.example.org/CCPD/api/reports/upload.

	SET CISCAT_OPTS=-nrf -ui
These options ensure only the ARF report file format is generated by the assessment process and SSL certificate warnings/errors are ignored when uploading the generated ARF assessment reports to the designated Dashboard.

	SET AUTHENTICATION_TOKEN=[Generate_An_Authentication_Token_In_CCPD]
To generate the token, please follow the instructions at [Establish authentication with Assessor](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#establishAuthWithAssessor) section from the Dashboard Deployment guide.

Replace **[Generate_An_Authentication_Token_In_CCPD]** with the Authentication Token generated by an "API" user in the CIS-CAT Pro Dashboard to which the CIS-CAT assessment reports will be uploaded to.


### Validate the Install ###
To test the setup, log into one of the target systems in the Workstation Group as a user capable of executing commands from an elevated command prompt, such as a domain admin.  Execute one of the following commands **from an elevated command prompt**, depending on which **.bat** file you intend to use (**cis-cat-centralized.bat** or **cis-cat-centralized-ccpd.bat**):

	C:\>\\CIS_HOST_SERVER\CIS\cis-cat-centralized.bat
	
	C:\>\\CIS_HOST_SERVER\CIS\cis-cat-centralized-ccpd.bat

Note that the **“CIS_HOST_SERVER”** value should be substituted with the actual name or IP of the machine configured as the CIS Host Server.

If successful, the above command will run an auto-assessment and result in output similar to the following:

![](https://i.imgur.com/7LV3Yce.png)

### Configuring the Scheduled Task via Group Policy ###
Perform the following steps to create and assign a Group Policy that will cause target systems in the Workstation Group to execute CIS-CAT via a Scheduled Task.  Note that some steps may vary slightly, depending on which version of Windows you are using.

1. Run `gpmc.msc` to modify the group policy
2. Select a group policy that is already targeted towards the computers that CIS-CAT needs to scan or create a new policy.
3. Next, create the scheduled task by navigating to **Computer Configuration -> Preferences -> Control Panel Settings -> Scheduled Tasks.**  Once there, click on **Action -> New -> Scheduled Task (Windows Vista and Later)**. Fill in the name of the task.
4. When setting the user who will be running the task, click the **“Change User or Group”** button, and click the **“Locations”** button on the **“Select User or Group”** popup:

    ![](https://i.imgur.com/KCdqvEZ.png)
1. On the **“Locations”** popup, expand the domain selection, select **“Builtin”** and click OK:

    ![](https://i.imgur.com/icaKMog.png)
1. Returning to the **“Select User or Group”** window, enter **“SYSTEM”** in the **“Enter the object name to select”** box, and click the **“Check Names”** button.  Select **“OK”** to select the SYSTEM user:

    ![](https://i.imgur.com/fLXSZlH.png)
    
    When returned to the scheduled task window, the **“NT AUTHORITY\System”** user should be indicated in the **“When running the task, use the following user account”** box.
1. Ensure the **“Run whether user is logged on or not”** radio button is selected, and make sure **“Run with highest privileges”** is checked.  It should look similar to the below screen shot.  Note that the **“Do not store password.  The task will only have access to local resources.”** checkbox will automatically be checked and disabled.  The inability to store credentials in the scheduled task is the result of applying the patch for **Microsoft security update MS14-025**.

    ![](https://i.imgur.com/0gtyt4M.png)
1. Add in whatever scheduling is needed via the **Triggers** tab.  Then go to the **Actions** tab click New and specify the following settings:
   * Set the **Action** drop down to **Start a program**
   * Set **Program/script** to **cmd.exe**
   * Set **Add arguments(optional)** to one of the following values, depending on whether you want to use the `cis-cat-centralized.bat` file **or** the `cis-cat-centralized-ccpd.bat` file.  Replace `<CisHostServer>` with the fully qualified domain name or IP address of the *CIS-CAT Host Server* you setup previously:

		`/c \\<CisHostServer>\CIS\cis-cat-centralized.bat`
	
		**or**
	
		`/c \\<CisHostServer>\CIS\cis-cat-centralized-ccpd.bat`

Once these steps are implemented, the **New Action** Dialog will look similar to the following:

![](https://i.imgur.com/AESSqVw.png)

Click **OK**.  CIS-CAT is now scheduled to run on all computers that are associated with the group policy.  The CIS-CAT assessment reports will be stored in the reports location or Dashboard you specified in the `cis-cat-centralized.bat` or `cis-cat-centralized-ccpd.bat` file, respectively.

### Bandwidth Considerations ###
Through the deployment and testing of the CIS-CAT Centralized workflow, bandwidth utilization can reach approximately 300 MB of data for each machine invoking CIS-CAT.  This bandwidth utilization is the cost of invoking CIS-CAT over the network.

<a name="assessMultipleUnixLinuxTargets"></a>
## Assessing Multiple Unix/Linux Targets ##
Similar to the **“Assessing Multiple Windows Targets”** section above, it is possible to assess multiple Unix, Linux, MacOS, Debian, Solaris, SUSE, etc targets in an automated manner without installing CIS-CAT or the JRE on each target.  Either the `cis-cat-centralized.sh` script or the `cis-cat-centralized-ccpd.sh` script is intended to reside on a centralized file share (referred to as the *CIS Host Server* in this document) that is accessible by the computers to be assessed by CIS-CAT.  The choice of which of these two files to use depends on where the assessment reports are to be written.  If you want to send the assessment reports to a Reports folder on the *CIS Host Server*, then use the cis-`cat-centralized.sh` file.  If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD) you have already setup, you must use the `cis-cat-centralized-ccpd.bat` file instead.  See the **"Update cis-cat-centralized.sh"** and **"Update cis-cat-centralized-ccpd.sh"** sections that follow for more information.

### CIS Host Server ###
The *CIS Host Server* is where the CIS-CAT bundle (including the various Java Runtime Environments) and possibly the Reports are placed.  Configured target machines will access these resources to perform a self-assessment using CIS-CAT.

Using the default configuration, consider the root folder for this workflow to be located at `/cis`.  

1. The first setup step in setting up the *CIS Host Server* is to copy the required scripts to the root folder.  The four scripts which are required reside in the `
2. /Unix-Linux` folder of a CIS-CAT installation bundle:
   * cis-cat-centralized.sh **OR** cis-cat-centralized-ccpd.sh
   * detect-os-variant.sh
   * make-jre-directories.sh
   * map-to-benchmark.sh
1. The next step is to copy the `Assessor-CLI` folder, and its contents, contained in the unzipped bundle to the workflow's root folder.
2. The last step in setting up the *CIS Host Server* is to configure the JRE sub-folders. The **“cis-cat-centralized.sh”** and **“cis-cat-centralized-ccpd.sh”** scripts are configured with an option to create the **“jres”** subfolder and all OS-specific folders underneath it.  Run one of the following commands, depending on whether you are using the **“cis-cat-centralized.sh”** or the **“cis-cat-centralized-ccpd.sh”** script: 

	`/cis> ./cis-cat-centralized.sh --make-jre-directories`

	or

	`/cis> ./cis-cat-centralized-ccpd.sh --make-jre-directories`

The default configuration of the *CIS Host Server* folder structure should now be as follows:

	/cis

	/cis/Assessor-CLI
	/cis/Assessor-CLI/reports
	...

	/cis/cis-cat-centralized.sh OR /cis/cis-cat-centralized-ccpd.sh   <-- Copied from misc/Unix-Linux
	/cis/detect-os-variant.sh                                         <-- Copied from misc/Unix-Linux
	/cis/make-jre-directories.sh                                      <-- Copied from misc/Unix-Linux
	/cis/map-to-benchmark.sh                                          <-- Copied from misc/Unix-Linux
	
	/cis/jres
	/cis/jres/AIX
	/cis/jres/AIX/bin/java
	...
	/cis/jres/Debian
	/cis/jres/HPUX
	/cis/jres/Linux
	/cis/jres/OSX
	/cis/jres/RedHat
	/cis/jres/Solaris
	/cis/jres/SolarisSparc
	/cis/jres/SUSE

### Update cis-cat-centralized.sh ###
Once the *CIS Host Server* is setup, a few modifications must be made to either `cis-cat-centralized.sh` or `cis-cat-centralized-ccpd.sh`. If you want to write the assessment reports to the *CIS Host Server*, utilize the `cis-cat-centralized.sh` script and modify it as directed in this section.  If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD), skip this section and go to the **"Update cis-cat-centralized-ccpd.sh"** section, instead.

	CISCAT_DIR=/cis/Assessor-CLI
	REPORTS_DIR=/cis/Assessor-CLI/reports
	JRE_BASE=/cis/jres
CISCAT_DIR, REPORTS_DIR, and JRE_BASE should be configured to align with the *CIS Host Server* folder structure. 

	SSLF='0'
The script can be configured to execute either the **“Level 1”** or **“Level 2”** **profile** (if available), based on an environment variable value.  This variable is named `SSLF`, and may be set to either 0 or 1.  Setting the value to 0 results in CIS-CAT evaluating the "Level 1" profile, while setting the value to 1 results in CIS-CAT evaluating the “Level 2” profile.

### Update cis-cat-centralized-ccpd.sh ###
If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD) you have already setup, you must use the `cis-cat-centralized-ccpd.sh` file instead of the `cis-cat-centralized.sh` file.  Modify the `cis-cat-centralized-ccpd.sh` file as follows: 

	CISCAT_DIR=/cis/Assessor-CLI
	JRE_BASE=/cis/jres
CISCAT_DIR and JRE_BASE should be configured to align with the *CIS Host Server* folder structure. 

	CCPD_URL=http://[YOUR-SERVER]/CCPD/api/reports/upload
CCPD_URL is used to set the URL for the CIS-CAT Pro Dashboard API to which CIS-CAT assessment reports will be uploaded.  The resource for CIS-CAT Pro Dashboard upload is **ALWAYS** mapped to the `/api/reports/upload` location, so the path to the application is all that should be modified here.  For example: http://applications.example.org/CCPD/api/reports/upload.

	AUTHENTICATION_TOKEN=[Generate_An_Authentication_Token_In_CCPD]
To generate the token, please follow the instructions in [Establish authentication with Assessor](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Linux/#establishAuthWithAssessor) section from the Dashboard Deployment guide.

Replace **[Generate_An_Authentication_Token_In_CCPD]** with the Authentication Token generated by an "API" user in the CIS-CAT Pro Dashboard to which the CIS-CAT assessment reports will be uploaded to.

	SSLF='0'
The script can be configured to execute either the **“Level 1”** or **“Level 2”** **profile** (if available), based on an environment variable value.  This variable is named `SSLF`, and may be set to either 0 or 1.  Setting the value to 0 results in CIS-CAT evaluating the "Level 1" profile, while setting the value to 1 results in CIS-CAT evaluating the “Level 2” profile.

### Validate the Install ###
To test the setup, log into one of the target systems that has access to the *CIS Host Server* as either a root user or a user capable of executing commands using sudo.  Execute one of the following commands, depending on which **.sh** file you intend to use (**cis-cat-centralized.sh** or **cis-cat-centralized-ccpd.sh**):

	> /path/to/cis/cis-cat-centralized.sh

	or
	
	> /path/to/cis/cis-cat-centralized-ccpd.sh

Note that `/path/to/cis` represents the file system path to the *CIS Host Server* and should be modified as appropriate before running the command.

If successful, the above command will run an auto-assessment on the target system and indicate successfully completion of the assessment.

The CIS-CAT assessment reports will be stored in the reports location or Dashboard you specified in the `cis-cat-centralized.sh` or `cis-cat-centralized-ccpd.sh` file, respectively.

CIS-CAT users can now integrate the invocation of the **“cis-cat-centralized.sh”** or **“cis-cat-centralized-ccpd.sh”** script into a task scheduling system such as `cron`, to be executed on any schedule deemed prudent for organizational needs.  Configuration of a Unix/Linux-based scheduling tool is beyond the scope of this User’s Guide.

## CIS-CAT Pro Dashboard Integration ##

### Introduction ###

The CIS-CAT Pro Dashboard has the ability to automatically import assessment results from CIS-CAT Pro Assessor. There are a few possible methods to configure the integration of CIS-CAT Pro Assessor and CIS-CAT Pro Dashboard to enable the upload of assessment results to the CIS-CAT Pro Dashboard database. From CIS-CAT Pro Assessor v3 and v4, results reports can be uploaded from a single CIS-CAT assessment (using either the graphical user interface in v3 or command-line user interface in v3 or v4). Additionally, users scanning with the “centralized” method to assess multiple Windows or Unix/Linux targets in v3 or v4 can modify the supporting files to automatically upload the results to CIS-CAT Pro Dashboard.
 
In order for the CIS-CAT Pro Dashboard and CIS-CAT Pro Assessor to communicate and share assessment results, authentication/authorization must be configured. Once the CIS-CAT Pro Dashboard has been installed, follow the instructions to generate an Authentication Token that will be used to validate the authentication in supporting CIS-CAT Pro Assessor files.

In support of SCAP 1.2, CIS-CAT Pro Dashboard can generate assessment results in Asset Reporting Format (ARF). The ARF report supports assessed content created as SCAP 1.2 data-stream collection or XCCDF 1.2-based data streams. CIS Benchmark content is created as XCCDF 1.2-based data streams. 

### Direct command line usage ###
To upload a report to CIS-CAT Pro Dashboard with the command line, a connection between CIS-CAT Pro Assessor and Dashboard needs to be established first. <br/>Please follow the instructions in [Establish authentication with Assessor](https://cis-cat-pro-dashboard.readthedocs.io/en/stable/source/Dashboard%20Deployment%20Guide%20for%20Windows/#establishAuthWithAssessor) section from the Dashboard Deployment guide.

Add the generated token to the assessor-cli.properties file:

	# Allow for a "bearer" token to be generated in CIS-CAT Pro Dashboard, allowing upload of
	# generated ARF reports to the new database application.
	ciscat.post.parameter.ccpd.token=m9i0o2lrqno60dlq49qlln6gqrj2l7kt

Save the property file. 

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, automatically selecting the first profile.  Configure the application to not generate any physical report files, but to upload the results to CIS-CAT Pro Dashboard, ignoring any SSL certificate warnings:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -nrf -u https://ccpd.example.org/CCPD/api/reports/upload -ui

### Windows centralized CIS-CAT Pro Dashboard usage ###
To use `cis-cat-centralized-ccpd.bat` script, please follow [Assessing Multiple Windows Targets](#assessMultipleWindowsTargets).

### Unix/Linux centralized CIS-CAT Pro Dashboard usage ###
To use `cis-cat-centralized-ccpd.sh` script, please follow [Assessing Multiple Unix/Linux Targets](#assessMultipleUnixLinuxTargets).
