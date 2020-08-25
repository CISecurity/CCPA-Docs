Change Log
==========

![](http://i.imgur.com/5yZfZi5.jpg)


CIS-CAT Pro Assessor v4
---------------------------
See the CIS-CAT Pro Assessor Coverage Guide for information about supported benchmarks, OVAL schemas/test types, and scripting capabilities.

## CIS-CAT Pro Assessor, v4.0.23 ##
#### Release Date: August 25, 2020 ####


### Benchmark Coverage ###
- Debian Family Linux v1.0.0
- Fedora 19 Family v1.0.0
- Microsoft Windows 10 Enterprise Release 2004 v1.9.0

### CIS-CAT Pro Updates ###
- Resolved an issue with configuration results for MacOS for the Gatekeeper recommendation 2.6.2 check.

### Documentation ###
- Updated Linux centralized assessment workflow. Renamed "Assessing Multiple Windows and Linux" sections of the Configuration Guide to be prefaced with "Centralized".

## CIS-CAT Pro Assessor, v4.0.22 ##
#### Release Date: July 30, 2020 ####


### Benchmark Coverage ###
- Microsoft SQL Server 2008 R2 v1.7.0 - Final release *
- Microsoft SQL Server 2012 v1.6.0 - Final release *
- Microsoft SQL Server 2014 v1.5.0 - Final release *
- Microsoft SQL Server 2016 v1.2.0
- Microsoft SQL Server 2017 v1.1.0
- Microsoft SQL Server 2019 v1.1.0
- Oracle 18c v1.0.0
- SUSE Linux 15 Enterprise v1.0.0
- Ubuntu Linux 20.04 v1.0.0

### CIS-CAT Pro Updates ###
- Added support for Java versions 8.251 through 14. Imports to Dashboard will now be successful when imported via the API.
- Errors will no longer occur if the default sessions.properties file is removed or renamed.
- Resolved an error with vulnerability HTML report generation.
- SuSE 15 and Ubuntu 20.04 now supported for vulnerability assessments.
- Target system state resulting in a score of "Fail" on a configuration assessment HTML assessment report are now emphasized with color and text.
- The link to initiate a support request that appears on an HTML report has changed to URL location where Members can enter support issues cisecurity.org\support.
- Resolved an error with Windows 10 vulnerability assessments.
- Ubuntu vulnerability definitions are now saved in assessor folder in an unzipped format and ready for use. 

### Documentation ###
- Corrected steps for CIS Host Server setup in "Assessing Multiple Unix/Linux Targets" section.
- Third party license version number information maintained in license.file relevant to each release of CIS-CAT Pro Assessor v4.

\* CIS Benchmarks marked with a "Final release" above will be moved to End of Life in the following CIS-CAT release.

## CIS-CAT Pro Assessor, v4.0.21 ##
#### Release Date: June 30, 2020 ####


### Benchmark Coverage ###
- CentOS Linux 7 v3.0.0
- Microsoft Windows 8.1 v2.4.0
- Microsoft Windows Server 2012 v2.2.0
- Microsoft Windows Server 2012 R2 v2.4.0
- Microsoft Windows Server 2016 RTM (Release 1607) Benchmark v1.2.0
- Oracle Linux 7 v3.0.0
- Red Hat Enterprise Linux 7 v3.0.0
- VMware ESXi 6.7 v1.1.0
- The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/) for more information.
	- Microsoft Windows 7 Workstation

### CIS-CAT Pro Updates ###
- Issue resolved with upload to CIS-CAT Pro Dashboard for Cisco IOS assessment of a show tech file.
- Target system collected state information now shown in detail on the HTML configuration report for all operating systems in "Assessment Details" section under "Assessment".
- Improved efficiency of VMware ESXi 6.7 scan specific to recommendation 2.1.
- Use -bi option on command line to produce a text file (benchmarks-info.txt) list of benchmarks and profiles.
- Improvements to the assessment process when Mac addresses are unable to be collected.
- Added new properties to specify custom graphics for the footer of the cover page of an HTML report or to simply not show the default footer of the cover page.
- Resolved an exception when non-standard namespaces are found in automated assessment content. The information is now properly parsed and handled.
- Enhanced Microsoft Windows assessment process in some scenarios when searching file systems.
- Enhanced Microsoft Windows assessment process in some scenarios when utilizing check sums to evaluate file systems.
- Enhancements to Microsoft Windows assessment process when collecting Windows services for evaluation.
- Some unscored CIS recommendations are now presented on CIS-CAT configuration reports as "Manual" instead of "Informational". Manual recommendations require additional Member verification and cannot be fully automated.

	NOTE: Export results values for these recommendations will change from "informational" to "manual". This may effect organizational processes that convert results using txt or csv assessment result output.

### Documentation ###
- Information on interpreting the HTML configuration report included in the guide. 

## CIS-CAT Pro Assessor, v4.0.20 ##
#### Release Date: May 5, 2020 ####


### Benchmark Coverage ###
- Apple macOS 10.14 v1.0.0.1
- Apple macOS 10.15 v1.0.0.1
- Google Chrome Benchmark v1.3.0 removed, v2.0.0 included only
- Google Kubernetes Engine v1.1.0
- Microsoft SQL Server 2008 R2 Benchmark v1.6.0 - Final release
- Microsoft SQL Server 2012 v1.5.0.1 - Final release
- Microsoft SQL Server 2014 v1.4.0.1 - Final release
- Microsoft SQL Server 2016 v1.1.0.1
- Microsoft SQL Server 2017 v1.0.0.1
- Microsoft SQL Server 2019 v1.0.0.1
- Microsoft Windows 7 Workstation v3.2.0 - Final release
- Microsoft Windows Server 2008 R2 v3.2.0
- Oracle 12c v3.0.0
- PostgreSQL 12 v1.0.0
- VMware ESXi 6.7 Benchmark v1.0.1
- The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/) for more information.
	- Apple OSX 10.10
	- Apple OSX 10.11
	- Debian Linux 7
	- Microsoft Internet Explorer 10
	- Microsoft Windows XP Professional
	- Mozilla Firefox 24 ESR
	- Oracle Database Server 11g R2

NOTE: To import VMware ESXi 6.7 Benchmark v1.0.1 configuration reports to CIS-CAT Pro Dashboard, Members MUST upgrade to CIS-CAT Pro Dashboard v1.1.13.

CIS Benchmarks marked with a "Final release" above will be moved to End of Life in the following CIS-CAT release.

### CIS-CAT Pro Updates ###
- Assessor can now collect and interpret system registry values while assessing Windows target systems when values contain non-English characters.
- Due to EOL of Canonical's Ubuntu 12, CIS-CAT no longer officially supports vulnerability assessments for this version of the operating system.
- A new property (esxi.max.wait) allows configuration of the maximum timeout value for the execution of each machine state collection command during a VMWare assessment.
- A deprecated property, user.assigned.machine.name property, was removed from the assessor-cli.property file.
- Updated to include the latest JSON 1.1 vulnerability feed data.

### Documentation ###
- Step-by-step instructions for Windows Task scheduling removed and replaced with more generic guidance with the understanding that Members have multiple different environments.
- Modified "Configuration Guide" to be more specific about preferred versions of Java to utilize with CIS-CAT Pro.
- Additional information now available on property settings.

## CIS-CAT Pro Assessor, v4.0.19 ##
#### Release Date: March 25, 2020 ####


### Benchmark Coverage ###
- None

### CIS-CAT Pro Updates ###
- Corrected an error in the display of the header in csv-formatted assessment results.
- Corrected the display of the CCE ID field in csv-formatted assessment results.
- Resolved an error when assessing Microsoft Windows Server 2008 R2.
- When downloading the latest, supported vulnerability definitions using CIS-CAT Pro commands, Microsoft Windows Server 2019 will now be included. SuSe Linux definition collection has also been updated.
- Using the -npr option on the command line, configuration assessment results can be produced in json format.
- Default Java memory allocation increased to 2 GB (2048MB) in all assessor-cli.bat and .sh and centralized scripts. This will require 64 bit Java installation. When running 32 bit Java, the scripts will need to be updated to 1024 MB. The Documentation now includes recommendations to set WinRM memory allocation and verify the current setting on target systems.
- Assessor will no longer incur an error when a detected file is subsequently deleted during an assessment of a textfilecontent54_test OVAL test.
- Updated to include the latest JSON 1.1 vulnerability feed data.

### Documentation ###
- Default options available for configuration in the assessor-cli.properties file are now described in further detail in the online documentation. See the "Properties" section of the Configuration Guide.

## CIS-CAT Pro Assessor, v4.0.18 ##
#### Release Date: February 25, 2020 ####


### Benchmark Coverage ###
- CIS Debian Linux 10 Benchmark v1.0.0
- CIS Kubernetes Benchmark v 1.5.1
- CIS Microsoft SQL Server 2019 Benchmark v1.0.0
- CIS Microsoft Windows 10 Enterprise 1903 v1.7.1
- CIS Microsoft Windows 10 Enterprise 1909 v1.8.1
- CIS MongoDB 3.6 v1.0.0

### CIS-CAT Pro Updates ###
- Remote Window sessions can now successfully connect for an assessment when using versions of Java 9 and above. A "javax" exception will no longer occur.
- Remote Microsoft SQL database assessments will no longer end in error when executed from operating systems other than Microsoft where PowerShell was installed instead of default.
- Enhanced Linux assessment process to handle some large system values encountered.
- Assessments of Microsoft SQL databases will have improved connection success as additional environment analysis has been added to the process.
- Database JDBC connection strings now obfuscated in log files.
- An error was resolved for Cisco remote assessments.
- Updated to include the latest JSON 1.1 vulnerability feed data.

### Documentation ###
- Updated Windows endpoint remote configuration for WinRM in flowchart and IPv4 and IPv6 filter settings.
- Linux assessments where user home directories exist on an auto-mounted, large storage drive, will experience longer assessment duration as some benchmarks check will take longer to complete.

## CIS-CAT Pro Assessor, v4.0.17 ##
#### Release Date: January 29, 2020 ####


### Benchmark Coverage ###
- CIS Debian Linux 9 Benchmark v1.0.1
- CIS Fedora 28 Family Linux v1.0.0, intended for any Divertive Distribution of Linux.  Requires the "ignore.platform.mismatch" property be set to "true" in the Assessor's properties file.
- CIS Microsoft Windows Server 2019 Benchmark v1.1.0
- CIS Ubuntu Linux 18.04 v2.0.1

### CIS-CAT Pro Updates ###
- Updated to include the latest JSON 1.1 vulnerability feed data.

## CIS-CAT Pro Assessor, v4.0.16 ##
#### Release Date: January 15, 2020 ####


### Benchmark Coverage ###
- Microsoft Windows 10 Enterprise 1909 v1.8.0
- Microsoft Windows 10 Enterprise 1903 v1.7.0

### CIS-CAT Pro Updates ###
- Reduction in quantity of executables called during an assessment, which assists with whitelisting activities.
- Improvement to the tool's overall security posture with third party Python library upgrade to v3.7, utilized primarily during Windows assessments.
- Upgrade to 1.2.3 version of Logback third-party library, which facilitates assessor
 activity logging.
- Upgrade to 2.5.6 version of Apache Groovy third-party library.
- Customize graphics and styling for HTML assessment report formats.
- CIS-CAT Pro Assessor v4 now handles instances when file paths with spaces are encountered during the assessment process. Previously, the assessment would end abruptly with an exception.
- Linux users are no longer prompted incorrectly for Kerberos (not supported) credentials.
- Additional option added on the command line to display profile names for a given benchmark. Follow a "-b" option with a benchmark file path for the xccdf with the new "-bi" option to show the list of profiles found in that benchmark.
- Corrected an error when assessing with DISA STIG data stream content.


## CIS-CAT Pro Assessor, v4.0.15 ##
#### Release Date: December 19, 2019 ####


### Benchmark Coverage ###
- None

### CIS-CAT Pro Updates ###
- Linux assessments have been corrected with updated SCE scripts. Previous scripts inadvertently contained characters causing "unknown" results for some recommendations.

## CIS-CAT Pro Assessor, v4.0.14 ##
#### Release Date: December 18, 2019 ####


### Benchmark Coverage ###
- Controls Assessment Module - Implementation Group 1 for Microsoft Windows Server 2016 v1.0.0

### CIS-CAT Pro Updates ###
- Enhanced Linux assessment process accommodates large user IDs.
- Controls Assessment Module file name change to identify Microsoft Windows 10 v1.0.3.
- Updated to include the latest JSON 1.1 vulnerability feed data.


## CIS-CAT Pro Assessor, v4.0.13 ##
#### Release Date: December 4, 2019 ####


### Benchmark Coverage ###
- CIS CentOS Linux 8 Benchmark v1.0.0
- CIS Microsoft Windows 10 Enterprise Release 1809 Benchmark v1.6.1
- CIS Microsoft Windows Server 2019 Benchmark v1.0.1
- CIS Oracle Linux 8 Benchmark v1.0.0
- CIS Red Hat Enterprise Linux 8 Benchmark v1.0.0

### CIS-CAT Pro Updates ###
- Benchmarks are now sorted alphabetically when viewed on Linux CLI in interactive mode (using option -i).
- Linux assessments results for recommendation 5.3.4 are now accurate. 
- Updated to include the latest JSON 1.1 vulnerability feed data.

## CIS-CAT Pro Assessor, v4.0.12 ##
#### Release Date: October 31, 2019 ####


### Benchmark Coverage ###
- Alibaba Cloud Aliyun Linux 2 v1.0.0

### CIS-CAT Pro Updates ###
- An option maintained in the properties file has been added to compress assessment result files prior to automatic import to CIS-CAT Pro Dashboard v1.1.9+ via API.
- Benchmark version number is now displayed when using the command line in interactive mode.
- ARF XML and HTML report generation issue resolved for Windows 10 1803 remote assessments.
- Cisco IOS target system correct domain or IP is now correctly shown on the HTML and ARF XML.

**IMPORTANT:** To utilize the new option to compress assessment results on post to Dashboard, users must upgrade to CIS-CAT Pro Dashboard v1.1.9. See the assessor-cli.properties file for more information.

## CIS-CAT Pro Assessor, v4.0.11 ##
#### Release Date: September 25, 2019 ####


### Benchmark Coverage ###
- CIS Microsoft Windows Server 2019 v1.0.0
- CIS MS Windows 10 Enterprise 1809 v1.6.0

### CIS-CAT Pro Updates ###
- Updated to include the latest JSON 1.1 vulnerability feed data.

## CIS-CAT Pro Assessor, v4.0.10 ##
#### Release Date: August 27, 2019 ####


### Benchmark Coverage ###
- None

### CIS-CAT Pro Updates ###
- MS Windows 10 configuration assessment HTML report displays OVAL assessment collected system values, recommended Benchmark values and rule used to generate pass/fail result.
- Support for NIST vulnerability JSON data feeds.
- Additional enhancements Ubuntu 18.04 assessment process to ensure more accurate results.
- Major performance improvements (10-100% performance increase) for Linux assessment process, particularly where a target has an attached a mounted file system. Additional option to exclude mounted file system, when necessary, for Linux only.
- Updated to latest NVD CVE feeds for up-to-date display of CVE information, including CVSS base scores and vector strings in HTML Reports.

## CIS-CAT Pro Assessor, v4.0.9 ##
#### Release Date: July 25, 2019 ####


### Benchmark Coverage ###
- PostgreSQL 11 v1.0.0
- Debian Linux v2.0.1

### CIS-CAT Pro Updates ###
- Updated to latest NVD CVE feeds for up-to-date display of CVE information, including CVSS base scores and vector strings in HTML Reports.  This update includes the 2019 feed.
- CIS-CAT Pro Assessor v4 vulnerability reports for Windows Server 2008 R2 can now import successfully into CIS-CAT Pro Dashboard.

## CIS-CAT Pro Assessor, v4.0.8 ##
#### Release Date: June 28, 2019 ####


### Benchmark Coverage ###
- None

### CIS-CAT Pro Updates ###
- Cisco IOS configuration assessment process enhanced to accommodate additional configuration scenarios
- Enhanced Ubuntu 18.04 configuration process to ensure more accurate results
- The unix/linux centralized scripts have been corrected to refer to the proper CIS-CAT Pro Assessor jar file
- Correction to linux centralized script for Debian operating systems
- Linux centralized scripts can now be used to assess Mac OS 10.13
- CIS-CAT Pro Assessor v4 vulnerability reports for Windows Server 2012 can now import successfully into CIS-CAT Pro Dashboard
- New section added to Controls Assessment Module documentation to provide information on remediation steps for automated checks
- Debian operating systems are now properly detected and assessed on local assessments and when pairing with external application build scripts


## CIS-CAT Pro Assessor, v4.0.7 ##
#### Release Date: June 3, 2019 ####


### Benchmark Coverage ###
- Debian Linux 8 Benchmark v2.0.0.1

### CIS-CAT Pro Updates ###
-  Error corrected for local Linux/Unix/Mac OS configuration assessments. Results will now be accurate for recommendations referring to files or file directories.

## CIS-CAT Pro Assessor, v4.0.6 ##
#### Release Date: May 29, 2019 ####


### Benchmark Coverage ###
- PostgreSQL 10 v1.0.0
- NGINX v1.0.0
- Mac OS 10.13 with OVAL support
- Google Chrome v75 v2.0.0
- MS SQL Server 2017 v1.0.0
- MS SQL Server 2016 v1.1.0
- MS SQL Server 2014 v1.4.0
- MS SQL Server 2012 Benchmark v1.5.0

### CIS-CAT Pro Updates ###
-  Consumers can now try V4 command line application with 3 Benchmarks (Ubuntu, Windows 10 Enterprise, Chrome) by downloading V4 Lite. Users can assess endpoints using Controls Assessment Module for Windows 10 Enterprise Implementation Group 1 for Controls V7.1.
-  Enhanced Debian 8 assessment process now produces accurate results for recommendations 1.5.1, 1.5.3, 3.1.1, 3.1.2 and 3.2.1 to 3.2.9.
-  Enhanced Ubuntu Linux assessment process accommodates large system group IDs.
-  Pass/fail assessment results for Windows 10 1803 now include the OVAL evidence.
-  Assess a Windows 10 endpoint with the Controls Assessment Module for Controls 7.1 Implementation Group 1.
-  Assessment result default file descriptions now only include "ARF" on XML configuration files.
-  Enhanced Debian 8 assessment process now produces more accurate results for recommendations 5.1.2 to 5.1.7.


## CIS-CAT Pro Assessor, v4.0.5 ##
#### Release Date: April 30, 2019 ####


### New Benchmarks ###
- None

### Benchmark Updates ###
- CIS Microsoft Windows 10 Enterprise 1803 v1.5.0.1 - scoring modification only for profile selection of ‘Windows 10 1803 Level 1 (L1) + BitLocker (BL) + Next Generation Windows Security (NG)’ or 'Windows 10 1803 Level 1 (L1) + BitLocker (BL)'

### CIS-CAT Pro Updates ###
-  Cisco IOS assessments will now produce accurate results when performing local and remote assessments.
-  Number only credentials for endpoints utilized in the configuration xml files are now valid.
-  A broader explanation and more generic referral to Level 1 Windows Benchmark recommendations that require consideration when remote scanning has been added to the online documentation. In order to remotely scan, users may need to except 2 or more recommendations.
-  Online documentation has been revised for Windows Endpoint Configuration to be more specific to users' environments.

## CIS-CAT Pro Assessor, v4.0.4 ##
#### Release Date: March 20, 2019 ####


### New Benchmarks ###
- CIS MS Windows 10 Enterprise Release 1803 Benchmark v1.5.0. Updates to centralized scripts and dissolvable bundle to accommodate the new Benchmark. CIS-CAT Pro will support the latest three published Windows Enterprise Benchmarks.
- CIS PostgreSQL 9.6 v1.0.0

### Benchmark Updates ###
- CIS Amazon Linux 2 v1.0.0.1 with updated Controls 7 mapping only
- CIS Microsoft IIS 10 Benchmark v1.1.1
- CIS PostgreSQL 9.5 v1.1.0.1

### CIS-CAT Pro Updates ###
-  Configuration XML files and sessions.properties files used to drive the assessment process can be encrypted.  See the **"File Encryption Options"** section of the User's Guide for more information.
-  Scripts are included for Linux and Windows environments to scan an entire domain when target machines have access to a network Java instance and CIS-CAT Pro Assessor. This is useful for members who want to use the assessor within a domain instead of remotely connecting to each target. See the **"Assessing Multiple Windows Targets"** and **"Assessing Multiple Unix/Linux Targets"** sections of the User's Guide for more information.
-  On screen message for local assessments will let users know if they lack privileges to execute the assessment.
-  The connection to remote endpoints has been modified to be more efficient.
-  Enhanced documentation with information on allowed characters used within the configuration XML file.
-  Linux configuration results have been corrected for reported issues on Linux CentOS recommendation 6.2.6.

## CIS-CAT Pro Assessor, v4.0.3 ##
#### Release Date: January 17, 2019 ####


### New Benchmarks ###
- CIS Debian Linux 9 Benchmark v1.0.0

### Benchmark Updates ###
- CIS Debian Linux 8 Benchmark v2.0.0
- CIS Microsoft IIS 10 Benchamrk v1.1.0
- CIS PostgreSQL 9.5 Benchmark v1.1.0

### CIS-CAT Pro Updates ###
-  Assessment result HTML reports now show the CIS Controls and CIS Sub-control version numbers when mapped to a CIS Benchmark recommendation. The CIS Control version is only available on some Benchmarks. Check the CIS website for more information. The title page of the report has also been enhanced to display long Benchmark names.
-  Scripts have been modified to allow an assessment to execute with OpenJDK, Java 9, Java 10, and Java 11.
-  User's Guide updated in section titled "Using CIS-CAT Pro Assessor CLI" to highlight requirement for a the user executing the application to have root, Administrator, or an equivalently privileged principal.
-  CIS-CAT Pro assessor has been enhanced to more efficiently work with OVAL content that uses XPath.
-  CIS Microsoft IIS 10 Benchmark has been corrected to properly collect assessment information. In prior versions, some users may have experienced false failures.
-  An issue was resolved with interactive values when users configured private keys with passphrases. The command line will now prompt users to enter a passphrase when the passphrase element is present and null in the Sessions or Config file. If the passphrase element does not exist for a target in the sessions or configuration xml, the command line will not prompt the user for an entry.
-  Report generation errors have been resolved for all versions of CIS Apple OSX 10.10, 10.11 and 10.12 Benchmark.    

## CIS-CAT Pro Assessor, v4.0.2 ##
#### Release Date: November 28, 2018 ####


### New Benchmarks ###
- None

### Benchmark Updates ###
- None

### CIS-CAT Pro Updates ###
-  Resolved User_object NPE/fatal error that occurs during some assessments.
-  Assessment results produced in csv format will now be modified per options set using the -D option.

## CIS-CAT Pro Assessor, v4.0.1 ##
#### Release Date: November 21, 2018 ####


### New Benchmarks ###
- CIS Amazon Linux 2 Benchmark v1.0.0

### Benchmark Updates ###
- CIS Benchmark for Windows Server 2016, v1.1.0

### CIS-CAT Pro Updates ###
-  Assessor-CLI.sh invalid Windows escape characters, preventing immediate run on Linux, have been removed.
-  ARF and OVAL vulnerability XML reports are now UTF-8 encoded to prevent invalid, non-UTF-8 characters from appearing in the report. The presence of these characters, can cause a problem when importing reports into other applications such as CIS-CAT Pro Dashboard.
- The environment command has been enhanced to handle variables configured over multiple lines.
- The ability to disable/enable schema validation now functions when configured in the assessor-cli.properties file.
- The creation of the Linux file item will no longer fail when a file size result is longer than maximum integer size.
- An update was made to the linux file collection process to account for the "xsi:nil=true" value in the filename element.

## CIS-CAT Pro Assessor, v4.0.0 ##
#### Release Date: October 26, 2018 ####
This is the initial release of CIS-CAT Pro Assessor v4 (CCPA), a command-line user interface enabling configuration and vulnerability assessment of endpoints.

### Assessor Updates ###
- Assessment of the system from which the Assessor is invoked.  This functionality mimics the host-based assessments from CIS-CAT v3.
- Assessment of remote Windows endpoints using WinRM and an "ephemeral" agent.
- Assessment of remote Unix/Linux endpoints using an SSH-based connection.
- Assessment of Cisco IOS network devices using an SSH-based connection.
- Support for the assessment of Security Content Automation Protocol (SCAP) 1.2 data-stream collections.
- Support for the assessment of XCCDF 1.2-based content.
- Support for the assessment of OVAL Definitions files, such as inventory and vulnerability definitions.
- Support for multiple report formats, such as the Asset Reporting Format and OVAL Results with System Characteristics in XML format, as well as HTML, CSV, or plain-text formats.
- Support for the upload of assessment results to CIS-CAT Pro Dashboard.