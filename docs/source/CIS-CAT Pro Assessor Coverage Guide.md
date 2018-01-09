![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor Coverage Guide #

## Introduction ##
This document provides information about the assessment capabilities of CIS-CAT Pro Assessor v4, such as OVAL test types, scripting capabilities, etc.


## OVAL Capabilities ##
International in scope and free for public use, OVAL is an information security community effort to standardize how to assess and report upon the machine state of computer systems. OVAL includes a language to encode system details, and an assortment of content repositories held throughout the community.

Tools and services that use OVAL for the three steps of system assessment — representing system information, expressing specific machine states, and reporting the results of an assessment — provide enterprises with accurate, consistent, and actionable information so they may improve their security. Use of OVAL also provides for reliable and reproducible information assurance metrics and enables interoperability and automation among security tools and services.

### Platform Independent ###
- Environment Variable (<5.8)
- Family
- File Hash (<5.8)
- File Hash (5.8+)
- LDAP (<5.7)
- LDAP (5.7+)
- SQL (5.7+)
- Text File Content (<5.4)
- Text File Content (5.4+)
- Variable
- XML File Content

### Microsoft Windows ###
- Access Token
- Audit Event Policy
- Audit Event Policy Subcategories
- Cmdlet
- File
- File Audited Permissions (<5.3)
- File Audited Permissions (5.3+)
- File Effective Rights (<5.3)
- File Effective Rights (5.3+)
- Group
- Group SID
- Interface
- Lockout Policy
- Password Policy
- Process (5.8+)
- Registry
- Registry Key Audited Permissions (<5.3)
- Registry Key Audited Permissions (5.3+)
- Registry Key Effective Rights (<5.3)
- Registry Key Effective Rights (5.3+)
- Service
- Service Effective Rights
- Shared Resource
- Shared Resource Audited Permissions
- Shared Resource Effective Rights
- SID
- SID SID
- UAC
- User
- User Rights
- User SID (5.5+)
- Volume
- WMI (<5.7)
- WMI (5.7+)
- WUA Update Searcher

### Microsoft IIS (Extension) ###
- Application Host Config
- Application Pool
- Site Bindings
- System Web
- Web Config

### Unix ###
- File
- Inetd
- Password
- Process (5.8+)
- Runlevel
- Shadow
- Symlink
- Sysctl
- Uname
- Xinetd

### Linux ###
- AppArmor Status
- DpkgInfo
- Inet Listening Servers
- Partition
- RPM Info
- SELinux Booleans
- Systemd Unit Property

### Mac OSX ###
TBD

### Cisco ASA ###
TBD

### Cisco IOS ###
- ACL
- BGP Neighbor
- Global
- Interface
- Line
- Router
- Routing Protocol Auth. Intf.
- Section
- SNMP
- SNMP Community
- SNMP Group
- SNMP Host
- SNMP User
- SNMP View
- Tclsh
- Version (<5.5)
- Version (5.5+)

### Other ###
- Shell Command (Extension, Platform Independent)
- Invalid User Home Directory Ownership (Extension, Linux)


## Scripting Capabilities ##
CIS-CAT Pro Assessor implements the Script Check Engine (SCE) check system, initially introduced as part of the [OpenSCAP](http://open-scap.org/page/SCE) project.  Using SCE in XCCDF documents allows administrators to use already-created scripts written in Bash, Windows Batch files, PowerShell, VBScript, etc. in benchmark recommendations.

CIS-CAT Pro Assessor supports using SCE usage with the following scripting languages:

- bash
- PowerShell
- Windows batch scripts
- VBScript


