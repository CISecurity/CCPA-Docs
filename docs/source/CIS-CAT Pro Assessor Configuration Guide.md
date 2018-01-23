![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor Configuration Guide #

## Introduction ##
Utilizing the CIS-CAT Pro Assessor CLI, users are capable of performing both host-based (local) assessments, as well as remote-based assessments.  In order to perform assessments of remote endpoints, certain configurations must be made.  The intent of this document is to serve as a guide for enabling systems for remote-based assessments using CIS-CAT Pro Assessor.

## Sessions ##
CIS-CAT Pro Assessor v4's remote assessment capability depends on the configuration of "sessions"; connection parameters used to create a secure connection to the remote endpoint.  A session configuration requires a number of entries, which will vary depending on the connection type.

### Connection Types ###
A number of different connection types exist to allow for maximum flexibility and coverage for the assessment of various endpoints, ranging from the local host to remote Windows, Unix, Linux, and Mac endpoints, as well as Cisco network devices.

| Type                   | Value      |   Description |
| -----------------------| ---------- | ------------- |
| Local                  | `local`    | Usage of a "local" session is for a host-based assessment, mimicing the functionality of CIS-CAT Pro v3.  Standalone or command-line applications (such as CIS-CAT Pro Assessor CLI) may use the local session to continue host-based assessments of benchmarks and/or OVAL definitions |
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

### Examples ###
The examples below provide insight into the creation of a `sessions.properties` file, which can then be consumed by CIS-CAT Pro Assessor CLI to provide connection configurations when assessing a particular benchmark.  By default, CIS-CAT Pro Assessor CLI will ALWAYS attempt to load a default configuration file located in the application's `config` folder, named `sessions.properties`.  For example, if CCPA is installed at `C:\CIS\Assessor-CLI`, a file named `C:\CIS\Assessor-CLI\config\sessions.properties` will be searched for and loaded (if found).  If no `sessions.properties` files are found or specified, a default `local` session will be used.

Configure a session for the local host:

    session.1.type=local

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

Configure a remote Linux session using a username/password:

    session.4.type=ssh
    session.4.host=ubuntu-test.example.org
    session.4.port=22
    session.4.user=ubuntu
    session.4.cred=s3cr3t3r!

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


- Connect to the instance either directly or through RDP
- Copy the `configure-winrm-ccpa.ps1` script to the endpoint
- When using an AWS instance, the public DNS name can be configured as the hostname:

	`$hostname = (New-Object System.Net.WebClient).DownloadString("http://169.254.169.254/2011-01-01/meta-data/public-hostname")`
- Or, uncomment the following line:

	`$hostname = "[HOSTNAME-or-IPADDRESS]"`
	
	and modify the value to an actual hostname or IP address.

NOTE:  This hostname value will be configured as the CN in the created self-signed certificate which CCPA will use during authentication/authorization.  If a certificate



## Unix/Linux Endpoint Configuration ##
CIS-CAT Pro Assessor assesses remote Unix/Linux targets via SSH connections.  Ensure the target system can be accessed via SSH and that the user connecting to the remote target is either the `root` user or a user granted privileges to execute commands using `sudo`.

## Cisco Network Device Endpoint Configuration ##
CIS-CAT Pro Assessor v4 can assess either the current running configuration of a Cisco network device, or an exported configuration file.

### Connecting to a Device ###
CIS-CAT Pro Assessor assesses Cisco network device targets via SSH connections.  Ensure the target system can be accessed via SSH and that the user connecting to the remote target is a privileged user.  When connecting to Cisco devices, CIS-CAT Pro Assessor will be configured to enter "privileged EXEC" mode, so any user connecting to the Cisco device via SSH must be granted appropriate permission to do so.

### Exported Configuration File ###
`show tech-support`

## Database Endpoint Configuration ##
JDBC

## (TODO) VMware ESXi Endpoint Configuration ##
Currently PowerCLI


### Extra configuration Options ###

	-sessions, --sessions <SESSIONS.PROPERTIES>
The `-sessions` option allows users to configure multiple endpoints for assessment of a benchmark.  The `sessions.properties` file configures CIS-CAT Pro Assessor for the assessment of remote endpoints by specifying remote hosts, ports, and credentials which the application will use for connection, collection and evaluation of benchmark recommendations and/or vulnerabilities.  See "Remote Assessment Capability" below for more information.

If no `sessions.properties` file exists or no connections are configured in the file, CIS-CAT Pro Assessor CLI will assess the local machine.