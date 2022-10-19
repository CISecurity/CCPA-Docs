CIS-CAT Pro Assessor Coverage Guide
===================================

![](http://i.imgur.com/5yZfZi5.jpg)


Introduction
------------
This document provides information about the assessment capabilities of CIS-CAT Pro Assessor v4, such as included benchmarks, OVAL test types, scripting capabilities, etc.

CIS Benchmark Coverage
----------------------
CIS currently distributes CIS-CAT with production support for the following benchmarks. The benchmarks utilize standards included in the Security Content Automation Protocol, such as the eXtensible Configuration Checklist Description Format (XCCDF) and the Open Vulnerability and Assessment Language (OVAL).

Note that any benchmark listed below which displays a bulleted list of "`id`:description" information are those benchmarks which contain "interactive values".  Please see the [CIS-CAT Pro Assessor CLI User's Guide](./User's%20Guide) for more information regarding configuration of these values.

For some older Windows platforms such as Microsoft Windows Server 2008 R2, it is required to be current with service pack updates in order for the assessment to process without error.

CIS-CAT Pro Assessor v4 strives to be a standards-based application focused on vendor-supported technology platforms and applications where OVAL coverage is available. The below technologies are supported. CIS-CAT Pro Assessor v4 supported CIS Benchmarks will be present in the benchmark directory of your downloaded CIS-CAT bundle and contain "oval" and "xccdf" in the filename. Please contact [CIS Support](https://www.cisecurity.org/support/) for additional coverage requests.

CIS Benchmarks that have reached end of life are no longer officially supported for use with CIS-CAT. As Members are working to upgrade systems within their organization to more current technology, CIS offers end of life CIS Benchmark automated assessment content on the CIS WorkBench. Navigate to [CIS WorkBench](https://workbench.cisecurity.org/files/2724) for more information.

The CIS Benchmarks are tested with the prior, official CIS-CAT version at the time automated Benchmark content is announced as supported in CIS-CAT. The CIS-CAT tool, on each release performs some regression testing, where possible, for most Benchmark versions released with the CIS-CAT bundle. Future and past CIS Benchmark versions for the technologies supported may work with the current or past CIS-CAT tool versions, but are not guaranteed and should be used at each organization's discretion.

- **CIS Aliyun Linux 2, v1.0.0**
- **CIS AlmaLinux OS 8 Benchmark, v2.0.0**
- **CIS Amazon Elastic Kubernetes Service (EKS) Benchmark, v1.1.0**
- **CIS Amazon Linux Benchmark, v2.0.0**
- **CIS Amazon Linux 2 Benchmark, v2.0.0**
- **CIS Amazon Linux 2 STIG Benchmark, v2.0.0**
- **CIS Apache Tomcat 9 Benchmark, v1.2.0**
- **CIS Apache Tomcat 9 Benchmark, v1.0.0**
- **CIS Apple macOS 10.15 Benchmark, v2.1.0**
- **CIS Apple macOS 11.0 Benchmark, v2.1.0**
- **CIS Apple macOS 12.0 Benchmark, v1.1.0**
- **CIS Azure Compute Microsoft Windows Server 2019 v1.0.0**
- **CIS Azure Kubernetes Service (AKS) v1.1.0**
- **CIS CentOS Linux 6 Benchmark, v3.0.0**
- **CIS CentOS Linux 7 Benchmark, v3.1.2**
- **CIS Cisco IOS 15 Benchmark, v4.1.1**
- **CIS Cisco IOS 16 Benchmark, v1.1.2**
- **CIS Cisco IOS 17 Benchmark, v1.0.0**
- **CIS Debian Family Linux, v1.0.0**
- **CIS Debian Linux 9 Benchmark, v1.0.1**
- **CIS Debian Linux 10 Benchmark, v1.0.0**
- **CIS Debian Linux 11 v1.0.0**
- **CIS Fedora 19 Family Linux, v1.0.0**
- **CIS Fedora 28 Family Linux, v2.0.1**
		- NOTE:  Requires the "ignore.platform.mismatch" property be set to "true" in the Assessor's properties file.
- **CIS Google Chrome Benchmark, v2.1.0**
- **CIS Google Kubernetes Engine (GKE) Benchmark, v1.2.0**
- **CIS_Kubernetes V1.20 Benchmark, v1.0.1**
- **CIS_Kubernetes V1.23 Benchmark, v1.0.1**
- **CIS Kubernetes 1.24 v1.0.0**
- **CIS MIT Kerberos 1.10 Benchmark, v1.0.0**
- **CIS Microsoft Edge Benchmark, v1.1.0**
- **CIS Microsoft IIS 7 Benchmark, v1.8.0**
- **CIS Microsoft IIS 8 Benchmark, v1.5.0**
- **CIS Microsoft IIS 10 Benchmark, v1.1.1**
- **CIS Microsoft Internet Explorer 11 Benchmark, v1.0.0**
- **CIS Microsoft Intune for Windows 10 Release 2004 Benchmark, v1.0.1**
- **CIS Microsoft Office Access 2013 Benchmark, v1.0.1**
- **CIS Microsoft Office Access 2016 Benchmark, v1.0.1**
- **CIS Microsoft Office Excel 2013 Benchmark, v1.0.1**
- **CIS Microsoft Office Excel 2016 Benchmark, v1.0.1**
- **CIS Microsoft Office Outlook 2013 Benchmark, v1.1.0**
- **CIS Microsoft Office Outlook 2016 Benchmark, v1.1.0**
- **CIS Microsoft Office PowerPoint 2013 Benchmark, v1.0.1**
- **CIS Microsoft Office PowerPoint 2016 Benchmark, v1.0.1**
- **CIS Microsoft Office Word 2013 Benchmark, v1.1.0**
- **CIS Microsoft Office Word 2016 Benchmark, v1.1.0**
- **CIS Microsoft Office 2013 Benchmark, v1.1.0**
- **CIS Microsoft Office 2016 Benchmark, v1.1.0**
- **CIS Microsoft SQL Server 2016 Benchmark, v1.3.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft SQL Server 2017 Benchmark, v1.2.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft SQL Server 2019 Benchmark, v1.2.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft Windows 10 Enterprise, v1.12.0**
- **CIS Microsoft Windows 10 EMS Gateway, v1.1.0**
- **CIS Microsoft Windows 10 Stand-alone Benchmark, v1.0.1**
- **CIS Microsoft Windows 11 Enterprise, v1.0.0**
- **CIS Microsoft Windows Server 2008 (non-R2) Benchmark, v3.1.0**
- **CIS Microsoft Windows Server 2008 R2 Benchmark, v3.3.0**
- **CIS Microsoft Windows Server 2012 (non-R2) Benchmark, v2.4.0**
- **CIS Microsoft Windows Server 2012 R2 Benchmark, v2.6.0**
- **CIS Microsoft Windows Server 2016 RTM (Release 1607) Benchmark, v1.4.0**
- **CIS Microsoft Windows Server 2016 STIG Benchmark, v1.2.0**
- **CIS Microsoft Windows Server 2019 Benchmark, v1.3.0**
- **CIS Microsoft Windows Server 2019 STIG Benchmark, v1.1.0**
- **CIS Microsoft Windows Server 2022 Benchmark, v1.0.0**
- **CIS Microsoft Windows 8 Benchmark, v1.0.0**
- **CIS Microsoft Windows 8.1 Workstation Benchmark, v2.4.0**
- **CIS MongoDB 3.6, v1.1.0**
    - `xccdf_org.cisecurity_value_runnin_config_file.url`: MongoDB running configuration file (mongod.conf) location.
- **CIS MongoDB 4, v1.0.0**
- **CIS MongoDB 5, v1.1.0**
- **CIS Mozilla Firefox 38 ESR Benchmark, v1.0.0**
- **CIS NGINX Benchmark, v1.1.0**
- **Oracle Cloud Infrastructure Container Engine for Kubernetes(OKE) Benchmark v1.1.0**
- **CIS Oracle MySQL Community Server 5.7 Benchmark, v2.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: MySQL Server connection string.
	- `xccdf_org.cisecurity_value_repl.user`: MySQL replication user name.
- **CIS Oracle MySQL Enterprise Edition 5.7 Benchmark, v2.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: MySQL Server connection string.
	- `xccdf_org.cisecurity_value_repl.user`: MySQL replication user name.
- **CIS Oracle MySQL Enterprise Edition 8.0 Benchmark, v1.2.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: MySQL Server connection string.
	- `xccdf_org.cisecurity_value_repl.user`: MySQL replication user name.
- **CIS Oracle Database 18c Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: Oracle Database connection string.
	- `xccdf_org.cisecurity_value_listener.ora`: Path to the listener.ora file
- **CIS Oracle Database 19c Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: Oracle Database connection string.
	- `xccdf_org.cisecurity_value_listener.ora`: Path to the listener.ora file
- **CIS Oracle Linux 6 Benchmark, v2.0.0**
- **CIS Oracle Linux 7 Benchmark, v3.1.1**
- **CIS Oracle Linux 8 Benchmark, v2.0.0**
- **Palo Alto Firewall 9 Benchmark v1.0.1 (offline only)**
- **Palo Alto Firewall 10 Benchmark v1.0.0 (offline only)**
- **CIS PostgreSQL 9.5 Benchmark, v1.1.0.1**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS PostgreSQL 9.6 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS PostgreSQL 10 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS PostgreSQL 11 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS PostgreSQL 12 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS PostgreSQL 13 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- - **CIS PostgreSQL 14 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS Red Hat Enterprise Linux 6 Benchmark, v3.0.0**
- **CIS Red Hat Enterprise Linux 7 Benchmark, v3.1.1**
- **CIS Red Hat Enterprise Linux 7 STIG Benchmark, v2.0.0**
- **CIS Red Hat Enterprise Linux 8 Benchmark, v2.0.0**
- **CIS Red Hat Enterprise Linux 7 STIG Benchmark, v1.0.0**
- **CIS Red Hat OpenShift Container Platform Benchmark, v1.2.0**
- **CIS Rocky Linux 8 Benchmark, v1.0.0**
- **CIS SUSE Linux Enterprise 12 Benchmark, v3.1.0**
- **CIS SUSE Linux Enterprise 15 Benchmark, v1.1.1**
- **CIS Ubuntu Linux 14.04 LTS Benchmark, v2.0.0**
- **CIS Ubuntu Linux 16.04 LTS Benchmark, v2.0.0**
- **CIS Ubuntu Linux 18.04 LTS Benchmark, v2.1.0**
- **CIS Ubuntu Linux 20.04 LTS Benchmark, v1.1.0**
- **CIS Ubuntu Linux 20.04 LTS STIG Benchmark, v1.0.0**
- **CIS Ubuntu Linux 22.04 LTS Benchmark, v1.0.0**
- **CIS VMware ESXi 6.7 v1.2.0**
	- `xccdf_org.cisecurity.benchmarks_value_esxi.connection`: ESXi host connection string
- **CIS VMware ESXi 7.0 v1.1.0**
	- `xccdf_org.cisecurity.benchmarks_value_esxi.connection`: ESXi host connection string


Platform Coverage for Vulnerability Assessments
-----------------------------------------------
Using the `-vdd` command-line option, CIS-CAT Pro Assessor v4 is able to download the latest vulnerability definitions from various repositories.  These files can also be manually downloaded from the repositories and copied into a folder name "vulnerabilities" located within the same parent folder location as the "benchmarks" folder. If you manually download vulnerability definition files, you will need to create the "vulnerabilities" folder if it does not already exist.  A number of different platforms are officially supported by CIS-CAT Pro Assessor v4, including:


| Platform                         | Downloaded From                                                    |
|----------------------------------|--------------------------------------------------------------------|
| Microsoft Windows XP             | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows 7              | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows 8              | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows 8.1            | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows 10             | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows Server 2003    | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows Server 2008    | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows Server 2008 R2 | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows Server 2012    | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows Server 2012 R2 | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows Server 2016    | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Microsoft Windows Server 2019    | https://oval.cisecurity.org/repository/download/5.10/vulnerability |
| Red Hat Enterprise Linux         | https://www.redhat.com/security/data/oval                          |
| SuSE Linux Enterprise Server 9   | https://support.novell.com/security/oval                           |
| SuSE Linux Enterprise Server 10  | https://support.novell.com/security/oval                           |
| SuSE Linux Enterprise Server 11  | https://support.novell.com/security/oval                           |
| SuSE Linux Enterprise Server 12  | https://support.novell.com/security/oval
| SuSE Linux Enterprise Server 15  | https://support.novell.com/security/oval                           |
| Ubuntu Linux 14.04               | https://people.canonical.com/~ubuntu-security/oval                 |
| Ubuntu Linux 16.04               | https://people.canonical.com/~ubuntu-security/oval                 |
| Ubuntu Linux 18.04               | https://people.canonical.com/~ubuntu-security/oval
| Ubuntu Linux 20.04               | https://people.canonical.com/~ubuntu-security/oval                 |

OVAL Capabilities
-----------------
International in scope and free for public use, OVAL is an information security community effort to standardize how to assess and report upon the machine state of computer systems. OVAL includes a language to encode system details, and an assortment of content repositories held throughout the community.

Tools and services that use OVAL for the three steps of system assessment — representing system information, expressing specific machine states, and reporting the results of an assessment — provide enterprises with accurate, consistent, and actionable information so they may improve their security. Use of OVAL also provides for reliable and reproducible information assurance metrics and enables interoperability and automation among security tools and services.

### Platform Independent ###
| Test Name | Implemented? | Notes |
|------------------------------------|---|-------|
| Environment Variable (<5.8)        | Y ||
| Environment Variable (5.8+)        | N | In development|
| Family                             | Y ||
| File Hash (<5.8)                   | Y ||
| File Hash (5.8+)                   | Y ||
| LDAP (<5.7)                        | Y ||
| LDAP (5.7+)                        | N | Deprecated |
| SQL (<5.7+)                        | N | Deprecated |
| SQL (5.7+)                         | Y ||
| Text File Content (<5.4)           | Y ||
| Text File Content (5.4+)           | Y ||
| Unknown                            | Y ||
| Variable                           | Y ||
| XML File Content                   | Y ||

### Microsoft Windows ###
| Test Name | Implemented? | Notes |
|------------------------------------|---|-------|
| Access Token | Y ||
| Active Directory (<5.7) | N | On roadmap |
| Active Directory (5.7+)| N | In Development |
| Audit Event Policy | Y ||
| Audit Event Policy Subcategories | Y ||
| Cmdlet | Y ||
| DNSCache | N | On roadmap |
| File | Y ||
| File Audited Permissions (<5.3) | Y ||
| File Audited Permissions (5.3+) | Y ||
| File Effective Rights (<5.3) | Y ||
| File Effective Rights (5.3+) | Y ||
| Group | Y ||
| Group SID | Y ||
| Interface | Y ||
| Junction | Y ||
| License | Y ||
| Lockout Policy | Y ||
| Metabase | N | |
| NTUser | N | On roadmap |
| Password Policy | Y ||
| PEHeader | Y ||
| Port | Y ||
| Printer Effective Rights | N | |
| Process (<5.8) | Y ||
| Process (5.8+) | Y ||
| Registry | Y ||
| Registry Key Audited Permissions (<5.3) | Y ||
| Registry Key Audited Permissions (5.3+) | Y ||
| Registry Key Effective Rights (<5.3) | Y ||
| Registry Key Effective Rights (5.3+) | Y ||
| Service | Y ||
| Service Effective Rights | Y ||
| Shared Resource | Y ||
| Shared Resource Audited Permissions | Y ||
| Shared Resource Effective Rights | Y ||
| SID | Y ||
| SID SID | Y ||
| System Metric | Y ||
| UAC | Y ||
| User | Y ||
| User Rights | Y ||
| User SID (<5.5) | Y ||
| User SID (5.5+) | Y ||
| Volume | Y ||
| WMI (<5.7) | Y ||
| WMI (5.7+) | Y ||
| WUA Update Searcher | Y ||

### Unix ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| DNSCache                 | N ||
| File                     | Y ||
| File Extended Attribute  | Y ||
| Gconf                    | Y ||
| Inetd                    | Y ||
| Interface                | Y ||
| Password                 | Y ||
| Process (<5.8)           | N |  |
| Process (5.8+)           | Y ||
| Routing Table            | N | |
| Runlevel                 | Y ||
| SCCS                     | N |  |
| Shadow                   | Y ||
| Symlink                  | Y ||
| Sysctl                   | Y ||
| Uname                    | Y ||
| Xinetd                   | Y ||

### Linux ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| AppArmor Status | Y ||
| DpkgInfo | Y ||
| IfListeners| N | |
| Inet Listening Servers | Y ||
| Partition | Y ||
| RPM Info | Y ||
| RPM Verify | N | |
| RPM Verify File | N | |
| RPM Verify Package | N | |
| SELinux Booleans | Y ||
| SELinux Security Context | N | |
| Slackware PkgInfo| N | |
| Systemd Unit Dependency | Y ||
| Systemd Unit Property | Y ||

### Mac OSX ###
| Test Name                      | Implemented? | Notes |
|--------------------------------|--------------|-------|
| Account Info                   | Y ||
| Authorization DB               | Y ||
| CoreStorage                    | Y ||
| Disabled Service               | N | |
| DiskUtil                       | N | |
| File Vault                     | N | In development |
| Firmware Password              | N | In development |
| Gatekeeper                     | Y ||
| Inet Listening Servers (<5.10) | N | |
| Inet Listening Servers (5.10+) | N | |
| Install History                | N | |
| Keychain                       | Y | |
| Launchd                        | Y ||
| Nvram                          | N |  |
| Nvram (5.12)                   | N |  |
| Plist (<5.10)                  | Y ||
| Plist (5.10)                   | Y ||
| Plist (5.11+)                  | Y ||
| Profiles                       | Y ||
| Pwpolicy (<5.9)                | N | |
| Pwpolicy (5.9+)                | N | |
| Pwpolicy (5.12+)               | N | |
| Rlimit                         | Y ||
| Software Update                | N | |
| System Profiler                | N | |
| System Setup                   | N | |

### Cisco ASA ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| ACL            | N | In backlog|
| Class Map      | N | In backlog|
| Interface      | N | In backlog|
| Line           | N | In backlog|
| Policy Map     | N | In backlog|
| Service Policy | N | In backlog|
| SNMP Host      | N | In backlog|
| SNMP Group     | N | In backlog|
| SNMP User      | N | In backlog|
| TCP Map        | N | In backlog|
| Version        | N | In backlog|

### Cisco IOS ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| ACL                          | Y | Partial implementation |
| BGP Neighbor                 | Y ||
| Global                       | Y ||
| Interface                    | Y ||
| Line                         | Y ||
| Router                       | Y ||
| Routing Protocol Auth. Intf. | Y ||
| Section                      | Y ||
| SNMP                         | Y ||
| SNMP Community               | Y ||
| SNMP Group                   | Y ||
| SNMP Host                    | Y ||
| SNMP User                    | Y ||
| SNMP View                    | Y ||
| Tclsh                        | Y ||
| Version (<5.5)               | Y ||
| Version (5.5+)               | Y ||

### Microsoft IIS (Extension) ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| Application Host Config  | Y ||
| Application Pool         | Y ||
| Site Bindings            | Y ||
| System Web               | Y ||
| Web Config               | Y ||
| Appcmd                   | N | In development |
| Appcmd List Config       | N | In development |

### VMware ESXi (Extension) ###
| Test Name                 | Implemented? | Notes |
|---------------------------|--------------|-------|
| VMHost Acceptance Level       | Y |  |
| VMHost VIB                    | Y |  |
| VMHost Module                 | Y |  |
| VMHost Coredump               | Y |  |
| VMHost Web Server SSL         | Y |  |
| VMHost Authentication         | Y |  |
| VMHost Account                | Y |  |
| VMHost SNMP                   | N |  |
| VMHost Advanced Setting       | Y |  |
| VMHost Service                | Y |  |
| VMHost NTP Server             | Y |  |
| VMHost Lockdown               | Y |  |
| VMHost Firewall Exception     | Y |  |
| VMHost Bus Adapter            | Y |  |
| VMHost iSCSI Host Bus Adapter | N |  |
| VMHost vSwitch Policy         | Y |  |
| VM Advanced Setting           | Y |  |
| VM Device                     | Y |  |
| VM Hard Disk Device           | Y |  |
| VM Resource Config            | N |  |
| Virtual Distributed Switch    | Y |  |
| Virtual Distributed Switch Port Group | Y |  |

### Other ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| Shell Command            | Y            | Extension, Platform Independent |
| Invalid User Home Directory Ownership |Y| Extension, Linux|


Scripting Capabilities
----------------------
CIS-CAT Pro Assessor implements the Script Check Engine (SCE) check system, initially introduced as part of the [OpenSCAP](http://open-scap.org/page/SCE) project.  Using SCE in XCCDF documents allows administrators to use already-created scripts written in Bash, Windows Batch files, PowerShell, VBScript, etc. in benchmark recommendations.

CIS-CAT Pro Assessor supports using SCE usage with the following scripting languages:

- bash
- PowerShell
- Windows batch scripts
- VBScript

### Configuring SCE Checks
Configuring a recommendation's `<check>` element to be evaluated using a script, users must first note the namespace URI of the Script Check Engine, the filepath, relative to the CIS-CAT Pro Assessor "working" directory, of the script, and any input arguments necessary during the execution of the script.

An example from the CIS CentOS 7 benchmark illustrates an SCE check:

    <xccdf:check system="http://open-scap.org/page/SCE">
    	<check-import import-name="stdout"/>
    	<xccdf:check-export export-name="XCCDF_VALUE_REGEX" value-id="xccdf_org.cisecurity.benchmarks_value_4.1.6.3_var"/>
    	<check-content-ref href="sce/auditd.sh"/>
    </xccdf:check>

Note the key information:

- The `system` attribute on the XCCDF `check` element must have a value of `http://open-scap.org/page/SCE` to indicate this is an SCE check, 
- The `<check-import import-name="stdout"/>` line must exist to indicate to the SCE that information displayed on `stdout` is relevant, 
- Any arguments required by the script must be passed as environment variables using the XCCDF `check-export` element.
	- The `export-name` attribute represents the name of the environment variable used within the script being executed.  While not mandatory, the `export-name` *should* follow the naming convention `XCCDF_VALUE_(NAME)`.  These same environment variable names are those that are used within the script itself.
	- The `value-id` attribute represents the XCCDF `Value` to be used as the value of the environment variable passed as an argument to the script.
- The `check-content-ref` element *must* exist, containing an `href` attribute value that references the name of the script to be executed.  This `href` value can be a relative path, based on the "working" directory of the CIS-CAT Pro Assessor, or a full canonical path to the script to be executed.  Using the example content above, if the CIS-CAT Pro Assessor "working" directory (the folder in which CCPA is installed) is `/opt/CCPA/Assessor-CLI`, the `href` attribute value of `sce/auditd.sh` references the script residing at `/opt/CCPA/Assessor-CLI/sce/auditd.sh`

CIS-CAT Pro Assessor determines the execution environment based on the file extension of the script:

| Script Extension | SCE Execution Environment | Notes |
|------------------|---------------------------|-------|
| .sh              | bash                      ||
| .ps1             | PowerShell                | Efforts have been made so users should not need to change any PowerShell settings in order to run these scripts.  CIS-CAT Pro Assessor v4 calls PowerShell using the `-ExecutionPolicy bypass` option.  This will temporarily bypass the existing PowerShell execution policy just for the duration of each CCPA script’s run without changing the system’s overall PowerShell execution policy.  Additionally, the `Unblock-File` PowerShell command will be run against the scripts when CIS-CAT Pro Assessor calls them; this will result in CCPA's scripts remaining unblocked/trusted even after running the Assessment.  The use of the `-ExecutionPolicy bypass` and `Unblock-File` are meant to contribute to a smoother user experience, but it is important that users consider any policy and security implications for their organization prior to running CIS-CAT Pro Assessor. |
| .bat             | Windows Batch             ||
| .vbs             | VBScript                  ||


CIS Embedded Check Language (ECL)
---------------------------------
CIS-CAT Pro Assessor contains minimal implementation of CIS' proprietary Embedded Check Language (ECL).  A subset of the total available functionality has been developed, in order to support both local and remote assessment of Apple OSX benchmarks.

The following ECL constructs have been implemented:

- File Content
- Shell Command
- Platform

Note that further ECL implementation is tentative and may not be included in future releases.
