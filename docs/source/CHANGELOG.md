![](http://i.imgur.com/5yZfZi5.jpg)

# Change Log #

----------

## CIS-CAT Pro Assessor v4.0.0 ##
### New Benchmarks ###
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

### Benchmark Updates ###
N/A for the initial release

### Assessor Updates ###
This is the initial release of CIS-CAT Pro Assessor v4 (CCPA), a command-line user interface enabling configuration and vulnerability assessment of endpoints.  Major features included in this initial release are:

- Assessment of the system from which the Assessor is invoked.  This functionality mimics the host-based assessments from CIS-CAT v3.
- Assessment of remote Windows endpoints using WinRM and an "ephemeral" agent.
- Assessment of remote Unix/Linux endpoints using an SSH-based connection.
- Assessment of Cisco IOS network devices using an SSH-based connection.
- Assessment of exported Cisco IOS configuration files; a file exporting the output of the `show tech-support` command.
- Support for the assessment of Security Content Automation Protocol (SCAP) 1.2 data-stream collections.
- Support for the assessment of XCCDF 1.2-based content.
- Support for the assessment of OVAL Definitions files, such as inventory and vulnerability definitions.
- Support for multiple report formats, such as the Asset Reporting Format and OVAL Results with System Characteristics in XML format, as well as HTML, CSV, or plain-text formats.
- Support for the upload of assessment results to CIS-CAT Pro Dashboard.