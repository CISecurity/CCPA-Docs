![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor Coverage Guide #

## Introduction ##
This document provides information about the assessment capabilities of CIS-CAT Pro Assessor v4, such as included benchmarks, OVAL test types, scripting capabilities, etc.

## CIS Benchmark Coverage ##
CIS currently distributes CIS-CAT with production support for the following benchmarks. The benchmarks utilize standards included in the Security Content Automation Protocol, such as the eXtensible Configuration Checklist Description Format (XCCDF) and the Open Vulnerability and Assessment Language (OVAL).

 1. CIS Amazon Linux Benchmark, v2.0.0
 2. CIS CentOS Linux 6 Benchmark, v2.0.2
 3. CIS CentOS Linux 7 Benchmark, v2.1.1
 4. CIS Cisco IOS 12 Benchmark, v4.0.0
 5. CIS Cisco IOS 15 Benchmark, v4.0.0
 6. CIS Debian Linux 7 Benchmark, v1.0.0.1
 7. CIS Debian Linux 8 Benchmark, v1.0.0.1
 8. CIS Google Chrome Benchmark, v1.2.0
 9. CIS MIT Kerberos 1.10 Benchmark, v1.0.0
10. CIS Microsoft IIS 7 Benchmark, v1.8.0
11. CIS Microsoft IIS 8 Benchmark, v1.5.0
12. CIS Microsoft Internet Explorer 10 Benchmark, v1.1.0
13. CIS Microsoft Internet Explorer 11 Benchmark, v1.0.0
14. CIS Microsoft Office Access 2013 Benchmark, v1.0.1
15. CIS Microsoft Office Access 2016 Benchmark, v1.0.1
16. CIS Microsoft Office Excel 2013 Benchmark, v1.0.1
17. CIS Microsoft Office Excel 2016 Benchmark, v1.0.1
18. CIS Microsoft Office Outlook 2013 Benchmark, v1.1.0
19. CIS Microsoft Office Outlook 2016 Benchmark, v1.1.0
20. CIS Microsoft Office PowerPoint 2013 Benchmark, v1.0.1
21. CIS Microsoft Office PowerPoint 2016 Benchmark, v1.0.1
22. CIS Microsoft Office Word 2013 Benchmark, v1.1.0
23. CIS Microsoft Office Word 2016 Benchmark, v1.1.0
24. CIS Microsoft Office 2013 Benchmark, v1.1.0
25. CIS Microsoft Office 2016 Benchmark, v1.1.0
26. CIS Microsoft SQL Server 2008 R2 Benchmark, v1.3.0
27. CIS Microsoft SQL Server 2012 Benchmark, v1.2.0
28. CIS Microsoft SQL Server 2014 Benchmark, v1.1.0
29. CIS Microsoft Windows 10 Enterprise Release 1703 Benchmark, v1.3.0
30. CIS Microsoft Windows Server 2003 Benchmark, v3.1.0
31. CIS Microsoft Windows Server 2008 (non-R2) Benchmark, v3.0.1
32. CIS Microsoft Windows Server 2008 R2 Benchmark, v3.0.1
33. CIS Microsoft Windows Server 2012 (non-R2) Benchmark, v2.0.1
34. CIS Microsoft Windows Server 2012 R2 Benchmark, v2.2.1
35. CIS Microsoft Windows Server 2016 RTM (Release 1607) Benchmark, v1.0.0
36. CIS Microsoft Windows 7 Workstation Benchmark, v3.0.1
37. CIS Microsoft Windows 8 Benchmark, v1.0.0
38. CIS Microsoft Windows 8.1 Workstation Benchmark, v2.2.1
39. CIS Microsoft Windows XP Benchmark, v3.1.0
40. CIS Mozilla Firefox 24 ESR Benchmark, v1.0.0
41. CIS Mozilla Firefox 38 ESR Benchmark, v1.0.0
42. CIS Oracle MySQL Community Server 5.6 Benchmark, v1.0.0
43. CIS Oracle MySQL Enterprise Edition 5.6 Benchmark, v1.0.0
44. CIS Oracle MySQL Community Server 5.7 Benchmark, v1.0.0
45. CIS Oracle MySQL Enterprise Edition 5.7 Benchmark, v1.0.0
46. CIS Oracle Database 11g R2 Benchmark, v2.2.0
47. CIS Oracle Database 12c Benchmark, v2.0.0
48. CIS Oracle Linux 6 Benchmark, v1.0.0
49. CIS Oracle Linux 7 Benchmark, v2.0.0
50. CIS Red Hat Enterprise Linux 5 Benchmark, v2.2.0
51. CIS Red Hat Enterprise Linux 6 Benchmark, v2.0.2
52. CIS Red Hat Enterprise Linux 7 Benchmark, v2.1.1
53. CIS SUSE Linux Enterprise 11 Benchmark, v2.0.0
54. CIS SUSE Linux Enterprise 12 Benchmark, v2.0.0
55. CIS Ubuntu Linux 14.04 LTS Benchmark, v2.0.0
56. CIS Ubuntu Linux 16.04 LTS Benchmark, v1.0.0

**NOTE**:  Any benchmarks which utilized CIS' proprietary Embedded Check Language (ECL) are not yet supported in CIS-CAT Pro Assessor v4.  Further development will either implement these benchmarks using currently available scripting capabilities, or will be migrated to OVAL when platform coverage is expanded.

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


