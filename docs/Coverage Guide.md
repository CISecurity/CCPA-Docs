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

- **CIS Amazon Linux Benchmark, v2.0.0**
- **CIS Amazon Linux 2 Benchmark v1.0.0.1**
- **CIS Apple macOS 10.13 Benchmark, v1.0.0.1**
- **CIS Apple OSX 10.10 Benchmark, v1.2.0**
- **CIS Apple OSX 10.11 Benchmark, v1.1.0**
- **CIS Apple OSX 10.12 Benchmark, v1.0.0**
- **CIS CentOS Linux 6 Benchmark, v2.0.2**
- **CIS CentOS Linux 7 Benchmark, v2.2.0**
- **CIS Cisco IOS 12 Benchmark, v4.0.0**
- **CIS Cisco IOS 15 Benchmark, v4.0.0**
- **CIS Debian Linux 7 Benchmark, v1.0.0**
- **CIS Debian Linux 8 Benchmark, v2.0.0.1**
- **CIS Debian Linux 9 Benchmark, v1.0.0**
- **CIS Google Chrome Benchmark, v1.3.0**
- **CIS Google Chrome Benchmark, v2.0.0**
- **CIS MIT Kerberos 1.10 Benchmark, v1.0.0**
- **CIS Microsoft IIS 7 Benchmark, v1.8.0**
- **CIS Microsoft IIS 8 Benchmark, v1.5.0**
- **CIS Microsoft IIS 10 Benchmark, v1.1.1**
- **CIS Microsoft Internet Explorer 10 Benchmark, v1.1.0**
- **CIS Microsoft Internet Explorer 11 Benchmark, v1.0.0**
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
- **CIS Microsoft SQL Server 2008 R2 Benchmark, v1.5.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft SQL Server 2012 Benchmark, v1.5.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft SQL Server 2014 Benchmark, v1.4.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft SQL Server 2016 Benchmark, v1.1.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft SQL Server 2017 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: SQL Server connection string.
- **CIS Microsoft Windows 10 Enterprise Release 1703 Benchmark, v1.3.0**
- **CIS Microsoft Windows 10 Enterprise Release 1709 Benchmark, v1.4.0**
- **CIS Microsoft Windows 10 Enterprise Release 1803 Benchmark, v1.5.0.1**
- **CIS Microsoft Windows Server 2003 Benchmark, v3.1.0**
- **CIS Microsoft Windows Server 2008 (non-R2) Benchmark, v3.1.0**
- **CIS Microsoft Windows Server 2008 R2 Benchmark, v3.1.0**
- **CIS Microsoft Windows Server 2012 (non-R2) Benchmark, v2.1.0**
- **CIS Microsoft Windows Server 2012 R2 Benchmark, v2.3.0**
- **CIS Microsoft Windows Server 2016 RTM (Release 1607) Benchmark, v1.0.0**
- **CIS Microsoft Windows 7 Workstation Benchmark, v3.1.0**
- **CIS Microsoft Windows 8 Benchmark, v1.0.0**
- **CIS Microsoft Windows 8.1 Workstation Benchmark, v2.3.0**
- **CIS Microsoft Windows XP Benchmark, v3.1.0**
- **CIS Mozilla Firefox 24 ESR Benchmark, v1.0.0**
- **CIS Mozilla Firefox 38 ESR Benchmark, v1.0.0**
- **CIS NGINX Benchmark, v1.1.0**
- **CIS Oracle MySQL Community Server 5.6 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: MySQL Server connection string.
	- `xccdf_org.cisecurity_value_repl.user`: MySQL replication user name.
- **CIS Oracle MySQL Enterprise Edition 5.6 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: MySQL Server connection string.
	- `xccdf_org.cisecurity_value_repl.user`: MySQL replication user name.
- **CIS Oracle MySQL Community Server 5.7 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: MySQL Server connection string.
	- `xccdf_org.cisecurity_value_repl.user`: MySQL replication user name.
- **CIS Oracle MySQL Enterprise Edition 5.7 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: MySQL Server connection string.
	- `xccdf_org.cisecurity_value_repl.user`: MySQL replication user name.
- **CIS Oracle Database 11g R2 Benchmark, v2.2.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: Oracle 11g R2 Server connection string.
	- `xccdf_org.cisecurity_value_listener.ora`: Path to the listener.ora file
- **CIS Oracle Database 12c Benchmark, v2.1.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: Oracle Database connection string.
	- `xccdf_org.cisecurity_value_listener.ora`: Path to the listener.ora file
- **CIS Oracle Linux 6 Benchmark, v1.0.0**
- **CIS Oracle Linux 7 Benchmark, v2.0.0**
- **CIS PostgreSQL 9.5 Benchmark, v1.1.0.1**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS PostgreSQL 9.6 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS PostgreSQL 10 Benchmark, v1.0.0**
	- `xccdf_org.cisecurity_value_jdbc.url`: PostgreSQL Database connection string.
- **CIS Red Hat Enterprise Linux 5 Benchmark, v2.2.0**
- **CIS Red Hat Enterprise Linux 6 Benchmark, v2.0.2**
- **CIS Red Hat Enterprise Linux 7 Benchmark, v2.1.1**
- **CIS SUSE Linux Enterprise 11 Benchmark, v2.0.0**
- **CIS SUSE Linux Enterprise 12 Benchmark, v2.0.0**
- **CIS Ubuntu Linux 14.04 LTS Benchmark, v2.0.0**
- **CIS Ubuntu Linux 16.04 LTS Benchmark, v1.0.0**
- **CIS Ubuntu Linux 18.04 LTS Benchmark, v1.0.0**

**NOTE**:  Any benchmarks which utilized CIS' proprietary Embedded Check Language (ECL) are not yet supported in CIS-CAT Pro Assessor v4.  Further development will either implement these benchmarks using currently available scripting capabilities, or will be migrated to OVAL when platform coverage is expanded.

Platform Coverage for Vulnerability Assessments
-----------------------------------------------
Using the `-vdd` command-line option, CIS-CAT Pro Assessor v4 is able to download the latest vulnerability definitions from various repositories.  A number of different platforms are officially supported by CIS-CAT Pro Assessor v4, including:


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
| Red Hat Enterprise Linux         | https://www.redhat.com/security/data/oval                          |
| SuSE Linux Enterprise Server 9   | https://support.novell.com/security/oval                           |
| SuSE Linux Enterprise Server 10  | https://support.novell.com/security/oval                           |
| SuSE Linux Enterprise Server 11  | https://support.novell.com/security/oval                           |
| SuSE Linux Enterprise Server 12  | https://support.novell.com/security/oval                           |
| Ubuntu Linux 12.04               | https://people.canonical.com/~ubuntu-security/oval                 |
| Ubuntu Linux 14.04               | https://people.canonical.com/~ubuntu-security/oval                 |
| Ubuntu Linux 16.04               | https://people.canonical.com/~ubuntu-security/oval                 |
| Ubuntu Linux 18.04               | https://people.canonical.com/~ubuntu-security/oval                 |

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
| DNSCache                 | N | On roadmap |
| File                     | Y ||
| File Extended Attribute  | Y ||
| Gconf                    | Y ||
| Inetd                    | Y ||
| Interface                | Y ||
| Password                 | Y ||
| Process (<5.8)           | N | On roadmap |
| Process (5.8+)           | Y ||
| Routing Table            | N | On roadmap |
| Runlevel                 | Y ||
| SCCS                     | N | On roadmap |
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
| IfListeners| N | On roadmap|
| Inet Listening Servers | Y ||
| Partition | Y ||
| RPM Info | Y ||
| RPM Verify | N | On roadmap|
| RPM Verify File | N | On roadmap|
| RPM Verify Package | N | On roadmap|
| SELinux Booleans | Y ||
| SELinux Security Context | N | On roadmap|
| Slackware PkgInfo| N | On roadmap|
| Systemd Unit Dependency | Y ||
| Systemd Unit Property | Y ||

### Mac OSX ###
| Test Name                      | Implemented? | Notes |
|--------------------------------|--------------|-------|
| Account Info                   | Y | |
| Authorization DB               | Y | |
| CoreStorage                    | Y | |
| DiskUtil                       | N | In development|
| Gatekeeper                     | Y ||
| Inet Listening Servers (<5.10) | N | In development|
| Inet Listening Servers (5.10+) | N | In development|
| Keychain                       | Y | |
| Launchd                        | Y ||
| Nvram                          | N | In development|
| Plist (<5.10)                  | Y ||
| Plist (5.10)                   | Y ||
| Plist (5.11+)                  | Y ||
| Pwpolicy (<5.9)                | N | In development|
| Pwpolicy (5.9+)                | N | In development|
| Rlimit                         | Y ||
| Software Update                | N | In development|
| System Profiler                | N | In development|
| System Setup                   | N | In development|

### Cisco ASA ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| ACL | N | In development|
| Class Map | N | In development|
| Interface | N | In development|
| Line | N | In development|
| Policy Map | N | In development|
| Service Policy | N | In development|
| SNMP Host | N | In development|
| SNMP Group | N | In development|
| SNMP User | N | In development|
| TCP Map | N | In development|
| Version | N | In development|

### Cisco IOS ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| ACL | Y | Partial implementation |
| BGP Neighbor | Y ||
| Global | Y ||
| Interface | Y ||
| Line | Y ||
| Router | Y ||
| Routing Protocol Auth. Intf. | Y ||
| Section | Y ||
| SNMP | Y ||
| SNMP Community | Y ||
| SNMP Group | Y ||
| SNMP Host | Y ||
| SNMP User | Y ||
| SNMP View | Y ||
| Tclsh | Y ||
| Version (<5.5) | Y ||
| Version (5.5+) | Y ||

### Microsoft IIS (Extension) ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| Application Host Config  | Y ||
| Application Pool         | Y ||
| Site Bindings            | Y ||
| System Web               | Y ||
| Web Config               | Y ||

### VMware ESXi (Extension) ###
| Test Name                | Implemented? | Notes |
|--------------------------|--------------|-------|
| VMHost Acceptance Level | N | In development |
| VMHost VIB | N | In development |
| VMHost Module | N | In development |
| VMHost Coredump | N | In development |
| VMHost Web Server SSL | N | In development |
| VMHost Authentication | N | In development |
| VMHost Account | N | In development |
| VMHost SNMP | N | In development |
| VMHost Advanced Setting | N | In development |
| VMHost Service | N | In development |
| VMHost NTP Server | N | In development |
| VMHost Lockdown | N | In development |
| VMHost Firewall Exception | N | In development |
| VMHost Bus Adapter | N | In development |
| VMHost iSCSI Host Bus Adapter | N | In development |
| VMHost vSwitch Policy | N | In development |
| VM Advanced Setting | N | In development |
| VM Device | N | In development |
| VM Hard Disk Device | N | In development |
| VM Resource Config | N | In development |
| Virtual Port Group | N | In development |

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

CIS Embedded Check Language (ECL)
---------------------------------
CIS-CAT Pro Assessor contains minimal implementation of CIS' proprietary Embedded Check Language (ECL).  A subset of the total available functionality has been developed, in order to support both local and remote assessment of Apple OSX benchmarks.

The following ECL constructs have been implemented:

- File Content
- Shell Command
- Platform

Note that further ECL implementation is tentative and may not be included in future releases.
