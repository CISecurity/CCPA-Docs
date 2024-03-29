![](http://i.imgur.com/5yZfZi5.jpg)

# Change Log

---------------------------

## CIS-CAT Pro Assessor v4 - [Download from CIS WorkBench](https://workbench.cisecurity.org/download/cis-cat/pro)

See the CIS-CAT Pro Assessor Coverage Guide for information about supported benchmarks, OVAL schemas/test types, and scripting capabilities.

---------------------------
## CIS-CAT Pro Assessor, v4.36.0
#### Release Date: Nov. 21, 2023 ####


### Benchmark Coverage ###

- Amazon Elastic Kubernetes Service (EKS) v1.4.0
- Microsoft Intune for Office v1.0.0
- Microsoft Intune for Windows 10 v2.0.1
- Microsoft Intune for Windows 11 v2.0.1
- MongoDB 7 Benchmark v1.0.0
- Oracle Cloud Infrastructure Container Engine for Kubernetes(OKE) Benchmark v1.4.0
- Oracle MySQL Community Server 8.0 Benchmark v1.0.0
- Oracle MySQL Enterprise Edition 8.0 Benchmark v1.3.0

### Security ###

- Resolved security vulnerabilities present in embedded, third party dependencies for io.netty (now at 4.1.101)
- The main Assessor application has been signed with a renewed signing certificate.

### Application 

- The size of the release package has been reduced due to a reduction in libraries unnecessary for assessment activities
- The Assessor Lite release bundle has been updated to include the CIS Microsoft Windows 11 Enterprise Benchmark
- The GUI enhanced to show additional help text on ‘Assessment Options’ screen when utilizing the ‘Result Destination POST URL'

### Documentation 

- README.txt document updated. There are no known vulnerabilities at the time of this release.

---------------------------

## CIS-CAT Pro Assessor, v4.35.0 
Release Date: Oct. 25, 2023 

### Benchmark Coverage ###

- AlmaLinux OS 8 v3.0.0
- Apple macOS 11 v4.0.0
- Apple macOS 12 v3.0.0
- Apple macOS 13 v2.0.0
- Apple macOS 14 v1.0.0
- Azure Kubernetes Service (AKS) v1.4.0
- Microsoft Intune for Windows 10 v2.0.0
- Microsoft Intune for Windows 11 v2.0.0
- Microsoft Windows Server 2012 R2 v3.0.0
- Microsoft Windows Server 2012 v3.0.0
- Microsoft Windows Server 2016 STIG v2.0.0
- MongoDB 5 v1.2.0
- MongoDB 6 v1.1.0
- Oracle Linux 8 v3.0.0
- PostgreSQL 15 v1.1.0
- PostgreSQL 16 v1.0.0
- Red Hat Enterprise Linux 8 v3.0.0
- Rocky Linux 8 v1.1.0
- VMware ESXI 8 v1.0.0

### Security ###

- Resolved security vulnerabilities present in embedded, third party dependencies for jackson-databind (now at 2.15.3)

### Application 

- When running CIS-CAT Lite on a Microsoft Windows 11 operating system, the GUI will no longer pause when attempting to load CIS Benchmark Microsoft Windows 11 Benchmark
- Linux assessment processes improved to now handle file path spaces when a network share exists.
- CIS-CAT Assessor license validator updated to be compatible with new CIS formats in addition to previous formats
- When CIS-CAT Pro Dashboard is utilized, the GUI will now validate that the POST URL is valid. On screen help will offer suggestions on resolution

### Documentation 

- README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries has been updated
	- io.netty updated, but did not have available stable versions at time of release 
- Lite users are informed in the Configuration Guide that installed Java is required when utilizing Lite on an operating system other than Windows
- The configuration guide was updated to specify PowerShell version requirements for Microsoft Windows assessments

----------------------

## CIS-CAT Pro Assessor, v4.34.0 
Release Date: Sep. 28, 2023 

### Benchmark Coverage 

- Kubernetes v1.8.0
- Microsoft Edge Benchmark v2.0.0
- VMware ESXI 7.0 v1.3.0

The following CIS Benchmarks have been archived and are no longer officially supported. See the Coverage Guide for more information on CIS Benchmarks that have been archived. The “archive” terminology replaces the previous "end of life" terminology when referring to CIS Benchmarks removed from CIS-CAT.

- Aliyun Linux 2
- Centos Linux 6
- Debian 9
- Fedora 19
- Oracle Linux 6
- Red Hat Linux 6
- Ubuntu 14.04
- Ubuntu 16.04

### Security 

- Resolved security vulnerabilities present in embedded, third party dependencies for okhttp (now 4.11.0)  and okio-jvm (now at 3.5.0)

### Application 

- Resolved ‘unknown’ results for some Linux where the script execution by the default non-interactive shell did not execute from a full bash shell
- CIS-CAT releases designed for MacOS host deployment now include an embedded Java Runtime Environment (JRE) to support GUI activities. New options and interface for download of CIS-CAT from [CIS WorkBench](https://workbench.cisecurity.org/files). See [Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/) with section titled Obtain CIS-CAT Pro Assessor.
- The GUI application now properly auto detects Microsoft Windows 11 and appropriately suggests the Microsoft Windows 11 Benchmark within the release bundle instead of the Microsoft Windows 10 Benchmark.
- MacOS host system owners wishing to continue to manage their own Java and prefer a release without an embedded Java may now select the Mac button and “No Java” and “No GUI” options on the download of CIS-CAT from [CIS WorkBench](https://workbench.cisecurity.org/files). See [Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/) with section titled Obtain CIS-CAT Pro Assessor.

### Documentation 

- The README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries has been updated.
- Configuration Guide updated to be specific that a Tomcat assessment is only applicable to Linux
- Clarified Property table for sce.max.wait to indicate that timeout must be enabled on MacOS or Linux to utilize this property
- Updated Configuration Guide to provide more information on Docker configuration assessments

---------------------------

## CIS-CAT Pro Assessor, v4.33.0 
Release Date: Aug. 29, 2023 

### Benchmark Coverage 

- Apache Tomcat 10 v1.1.0
- Debian Linux 11 STIG v1.0.0
- Microsoft Office Enterprise v1.1.0
- Microsoft SQL Server 2016 v1.4.0
- Microsoft SQL Server 2017 v1.3.0
- Ubuntu Linux 20.04 LTS STIG v2.0.0

### Security 

- None

### Application 

- None

### Documentation 

- CIS-CAT releases designed for MacOS host deployment now include an embedded Java Runtime Environment (JRE) to support command line (CLI) activities. A host-installed JRE is no longer required in this instance. MacOS host system owners wishing to continue to manage their own Java and prefer a release without an embedded Java should use the Linux without embedded Java. New options and interface for download of CIS-CAT from **[CIS WorkBench](https://workbench.cisecurity.org/files)**. See **[Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/)** with section titled Obtain CIS-CAT Pro Assessor.

---------------------------

## CIS-CAT Pro Assessor, v4.32.0 
Release Date: Jul. 27, 2023 

### Benchmark Coverage 

- Apple macOS 11 v3.1.0
- Apple macOS 12 v2.1.0
- Apple macOS 13 v1.1.0
- Microsoft Windows 10 EMS Gateway v2.0.0
- Microsoft IIS 10 v1.2.1

### Security 

- Resolved security vulnerabilities present in embedded, third party dependencies for kotlin-stdlib (now v1.8.22) and cxf-rt-bindings (now v3.5.5)
- Additional obfuscation was applied to detailed assessment evidence in the HTML report for Linux CIS Benchmarks

### Application 

- None

### Documentation 

- Updated README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries
- Clarification added to the **[Oracle Database](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#OracleDatabase)** connection string section of the configuration guide in reference to the username utilized for connection strings
- CIS-CAT Pro Assessor’s **[software bill of materials (SBOM)](https://workbench.cisecurity.org/files/4551)** is now available for download separately in addition to within the release bundle.

---------------------------

## CIS-CAT Pro Assessor, v4.31.0 
Release Date: Jun. 27, 2023

### Benchmark Coverage 

- AKS-Optimized Azure Linux 2 v1.0.0
- Amazon Linux 2023 v1.0.0
- Docker v1.6.0
- Microsoft SQL Server 2019 v1.3.0
- Oracle 18c v1.1.0
- NGINX v2.0.1
- RedHat OpenShift Container Platform v4 v1.4.0
- Ubuntu Linux 20.04 LTS v2.0.1

### Security 

- None

### Application 

- A new property added in the Assessor-CLI.properties file offers an option, when utilized, that will allow Linux/macOS CIS Benchmark recommendation checks to execute up to the set duration for this property. The recommendation result will be marked unknown, scored as a fail result.  
- The Assessor-CLI.jar file, the main executable for all assessor processes, is now signed and provides the benefit for Members to validate code integrity.

### Documentation 

- Software Bill of Materials files have been renamed to SBOM_CIS_CAT_Pro_Assessor
- Updated README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries.

---------------------------

## CIS-CAT Pro Assessor, v4.30.0 
Release Date: May. 25, 2023 

### Benchmark Coverage 

- Amazon Elastic Kubernetes Service (EKS) v1.3.0
- Debian Linux 10 v2.0.0
- Kubernetes Benchmark v1.7.1
- Microsoft Windows 10 Standalone v2.0.0
- Microsoft Windows 11 Standalone v2.0.0
- Oracle Cloud Infrastructure Container Engine for Kubernetes(OKE) v1.3.0
- Palo Alto Firewall 9 v1.1.0
- Palo Alto Firewall 10 v1.1.0
- Palo Alto Firewall 11 v1.0.0
- Ubuntu Linux 20.04 LTS v2.0.0

### Security 

- None

### Application 

- Permissions have been set for cis-cat-centralized.sh and cis-cat-centralized-ccpd.sh and will persist for all versions of the Linux build when build is extracted on a Linux machine.

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.29.0 
Release Date: Apr. 27, 2023 

### Benchmark Coverage 

- Azure Compute Microsoft Windows Server 2019 v1.0.1
- Azure Kubernetes Service (AKS) v1.3.0
- Google Kubernetes Engine (GKE) v1.4.0
- Microsoft Windows Server 2016 v2.0.0
- Microsoft Windows Server 2019 v2.0.0
- Microsoft Windows Server 2022 v2.0.0
- MongoDB 6 v1.0.0
- MySQL 8.0 v1.2.1
- PostgreSQL 12 v1.1.0
- PostgreSQL 13 v1.1.0

### Security 

- None

### Application 

- An issue has been resolved for Linux centralized script. The correct Benchmarks are now selected when auto detect is turned on.
- Permissions pre-set to read and execute Assessor-CLI.sh for all versions of the Linux build
- Permissions pre-set to read and execute embedded java for versions including java
- HTML report updated to represent CIS Benchmark recommendations intentionally not mapped to a CIS Critical Control as “Explicitly Not Mapped”

### Documentation 

- Resolved incorrect link to external documentation in the configuration guide in the WinRM section
- Corrected an error where the “Documentation” folder containing the Software Bill of Materials (SBOM) was excluded.

---------------------------

## CIS-CAT Pro Assessor, v4.28.0 
Release Date: Mar. 28, 2023

### Benchmark Coverage 

- Cisco iOS 16 v2.0.0
- Cisco iOS 17 v2.0.0
- Kubernetes v1.7.0
- Microsoft SQL Server 2022 v1.0.0
- Microsoft Windows 10 Enterprise v2.0.0
- Microsoft Windows 11 Enterprise v2.0.0
- PostgreSQL 14 v1.1.0
- VMware ESXi 7.0 v1.2.0
- VMware ESXi 6.7 v1.3.0

### Security 

- Resolved security vulnerabilities present in embedded, third party dependency, snakeyaml. This library has moved to version 2.0.0.

### Application 

- Assessor’s base application has been updated from Groovy 2 to Groovy 3.
- The application’s base framework has been upgraded to from Gradle 6 to 7.
- The CIS SecureSuite license process has been modified to remove the dependency on Data Exchange Layer (DXL) communication fabric.

### Documentation 

- Updated README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries.

---------------------------

## CIS-CAT Pro Assessor, v4.27.0 
Release Date: Feb. 28, 2023

### Benchmark Coverage 

- None

### Security 

- None

### Application 

- The Linux centralized scripts have been updated to correctly map to the Ubuntu 22.04 CIS Benchmark
- The Microsoft Windows builds now contain only relevant Windows operational files.
- The Linux builds now contain only relevant Linux operational files.
- Linux bundles now have the option to be downloaded with an embedded Java. Centralized scripts will utilize the embedded java when this optional bundle has been downloaded. Correct permissions MUST be recursively applied to the jre folder in order for the assessment process to function. MacOS users should use the Linux version without Java. Find more information about available builds that can be [downloaded](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#obtain-cis-cat-pro-assessor) for CIS-CAT Pro Assessor.
- The centralized scripts in the Linux with Java CIS-CAT bundle have been modified to utilize the embedded Java.
- Command line console messaging for importing results to CIS-CAT Pro Dashboard have been improved

### Documentation 

- Updated README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries.
- CIS-CAT now delivers with a Software Bill of Materials (SBOM) located in the documentation directory
- The documentation directory now contains the licenses for third party libraries utilized by CIS-CAT
- The documentation on [obtaining CIS-CAT Pro Assessor](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#obtain-cis-cat-pro-assessor) has been updated with the new options for downloading CIS-CAT Pro Assessor with embedded Java.

---------------------------

## CIS-CAT Pro Assessor, v4.26.0 
Release Date: Jan. 25, 2023 

### Benchmark Coverage 

- Azure Server 2022 Compute Benchmark v1.0.0
- Microsoft Windows Intune for Windows 11 v1.0.0
- Oracle Database 19c v1.1.0

### Security 

- Updated README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries.
- Resolved security vulnerabilities present in embedded, third party dependency, jackson-databind. This library has moved to version 2.14.0.

### Application 

- GUI: The assessment progress bar has been corrected to coordinate with the actual progress of the assessment.

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.25.0 
Release Date: Dec. 20, 2022 

### Benchmark Coverage 

- Alma Linux 9 v1.0.0
- Microsoft IIS 10 v1.2.0
- Microsoft Office Enterprise v1.0.0
- NGINX v2.0.0
- Oracle Cloud Infrastructure Container Engine for Kubernetes(OKE) Benchmark v1.2.0
- Oracle Linux 9 v1.0.0
- PostgreSQL 15 Benchmark v1.0.0
- Red Hat OpenShift Container Platform Benchmark v1.3.0
- Rocky Linux 9 v1.0.0

The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the Coverage Guide for more information on CIS Benchmarks that have reached end of life.* The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the Coverage Guide for more information on CIS Benchmarks that have reached end of life.

- Amazon Linux v2.0.0
- Microsoft Internet Explorer 11 v1.0.0
- Microsoft IIS 7 v1.8.0
- Microsoft Office Access 2016 Benchmark, v1.0.1
- Microsoft Office Excel 2016 Benchmark, v1.0.1
- Microsoft Office Outlook 2016 Benchmark, v1.1.0
- Microsoft Office PowerPoint 2016 Benchmark, v1.0.1
- Microsoft Office Word 2016 Benchmark, v1.1.0
- Microsoft Office 2016 Benchmark, v1.1.0

### Security 

- Updated README.txt document for the list of suppressed third party security vulnerabilities from dependent libraries determined as “false positives” for multiple “commons…”, jcl-over-slf4j, and xmlschema-core jar files.
- Additional changes have further obscured security information for Linux assessments in assessment evidence text within the HTML and the *ARF.XML formatted configuration assessment output.
- Cisco IOS security information has been obscured in assessment evidence text within the HTML and the *ARF.XML formatted configuration assessment output. 
- Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/cp/GwThzTEn) for more information.

### Application 

- None

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.24.0 
Release Date: Nov. 30, 2022

### Benchmark Coverage 

- Amazon Elastic Kubernetes Service (EKS) v1.2.0
- Apple macOS 10.15 Catalina v3.0.0
- Apple macOS 11 Big Sur v3.0.0
- Apple macOS 12 Monterey v2.0.0
- Apple macOS 13 Ventura v1.0.0
- Microsoft Intune for Windows 10 v1.1.0
- Microsoft Windows 11 Standalone v1.0.0
- Red Hat Enterprise Linux 9 v1.0.0

### Security 

- An issue has been resolved where some security information for Linux assessments was exposed in assessment evidence text within the HTML and the *ARF.XML formatted configuration assessment output.
- Resolved security vulnerability present in embedded, third party dependency for postgresql-42.4.1.jar . This library has moved to postgresql-42.5.1.jar.

### Application 

- Assessor functions ( -vdd, -od, -cfg) to support vulnerability assessment have been removed. CIS-CAT Pro Assessor now exclusively performs configuration assessments primarily for CIS Benchmarks with automated assessment content. Please see our [knowledge base article](https://cisecurity.atlassian.net/l/cp/CLRHc4H4) for more information.
- CIS-CAT releases designed for Microsoft Windows deployment that also include GUI deploy with an embedded Java Runtime Environment (JRE) to support GUI and command line (CLI) activities. A host-installed JRE is no longer required in this instance. Linux host installation still require a JRE.
- The GUI software version has been upgraded to the latest available version.
- GUI: Automatic operating system detection and CIS Benchmark selection for Microsoft Windows Server 2016 local assessments
- An issue has been corrected for some Linux configuration assessments improving assessment results for RHEL 8 and 9, Debian 11, Ubuntu 22.04, CentOS 8, Oracle 8, Rocky 8, and Alma 8.
- New options and interface for download of CIS-CAT from [CIS WorkBench](https://workbench.cisecurity.org/files). See [Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/) with new section titled Obtain CIS-CAT Pro Assessor.

### Documentation 

- Updated [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/) to remove “Platform Coverage for Vulnerability Assessments”.  Updated [User Guide Assessor](https://ccpa-docs.readthedocs.io/en/latest/User%20Guide%20-%20Assessor/) to remove instructions for performing vulnerability assessments. CIS-CAT Pro Assessor now exclusively performs configuration assessments primarily for CIS Benchmarks with automated assessment content.
- Configuration Guide updated for [Properties](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#properties) section for setting default GUI report and report output options, adding support Windows 2016
- [User Guide](https://ccpa-docs.readthedocs.io/en/latest/User%20Guide%20-%20Assessor/#graphical-user-interface-gui) updated to include Microsoft Windows Server 2016 in Benchmark auto detection.
- Updated [Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/) with new section titled `Obtain CIS-CAT Pro Assessor` on options to download CIS-CAT from CIS WorkBench. CIS now offers “build your own” options based on operating system and interface type.

---------------------------

## CIS-CAT Pro Assessor, v4.23.0 
Release Date: Oct. 28, 2022 

### Benchmark Coverage 

- Azure Kubernetes Service (AKS) Benchmark v1.2.0
- Google Kubernetes Engine (GKE) Benchmark  V1.3.0

### Security 

- Resolved security vulnerability present in embedded, third party dependency for jackson-databind. This library has moved to jackson-databind-2.13.4.jar.

### Application 

- GUI: Set default selections in the GUI via the assessor-cli.properties file for:
	- Report output formats (HTML, csv, txt, json,xml)
	- Report output locations (share drives)
	- Report posting location for CIS-CAT Pro Dashboard result importing
- GUI: Automatic operating system detection and CIS Benchmark selection for Microsoft Windows
	- Supports local assessments only from the GUI
	- Supports Microsoft Windows:
		- 10 Enterprise
		- Server 2012r2
		- Server 2012 
		- Server 2019
		- Server 2022

### Documentation 

- Quick Start Guide now available for frequent support topics
- [Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#properties) updated for Properties section for setting default GUI report and report output options.
- [User Guide](https://ccpa-docs.readthedocs.io/en/latest/User%20Guide%20-%20Assessor/#graphical-user-interface-gui) updated on setting default report options in the GUI.

---------------------------

## CIS-CAT Pro Assessor, v4.22.0 
Release Date: Sep. 30, 2022

### Benchmark Coverage 

- Apache Tomcat 9 v1.2.0
- Apache Tomcat 10 v1.0.0
- Azure Compute Microsoft Windows Server 2019 v1.0.0
- Debian Linux 11 v1.0.0
- Kubernetes 1.24 v1.0.0
- Microsoft Edge v1.1.0

### Security 

- Resolved security vulnerabilities present in embedded, third party dependencies. Please see the related [knowledge base article](https://cisecurity.atlassian.net/l/cp/tuwKj3XB) for more information.

### Application 

- Corrected an issue where the assessed Linux system’s IP did not show correctly on CIS-CAT output reports.
- Configuration assessment logging information has been enhanced for Oracle Databases.
- Resolved ‘unknown’ results for Debian 11 configuration assessment results.

### Documentation 

- The instructions for Assessor V4 Service have been removed and included in the final release of the standalone application of CIS-CAT Pro Assessor v4 Service version 1.22.0. CIS will no longer offer support for this standalone application. Please read our [knowledge base article](https://cisecurity.atlassian.net/l/cp/UfvH2cpK) to learn more. This remote assessment functionality will be embedded as a standard function within CIS-CAT Pro Dashboard v3.0.0, available in Q4 2022.

---------------------------

## CIS-CAT Pro Assessor, v4.21.0 
Release Date: Aug. 30, 2022 

### Benchmark Coverage 

- Microsoft Windows 10 Stand-alone v1.0.1
- Ubuntu Linux 22.04 LTS v1.0.0

### Security 

- Resolved security vulnerability present in embedded, third party dependency for postgresql.jar. This library has moved from 42.3.5 to 42.4.1.

### Application 

- Resolved an issue where Cisco IOS reports showed a null prefix.
- Updated automated configuration assessment functions to support additional automation for Microsoft Windows 10 Stand-alone Benchmark (non-domain joined).

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.20.0 
Release Date: July 26, 2022 

### Benchmark Coverage 

- Apple macOS 10.15 Catalina v2.1.0
- Apple macOS 11.0 Big Sur v2.1.0
- Apple macOS 12.0 Monterey v1.1.0
- Microsoft Windows 10 Stand-alone Benchmark v1.0.0

The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the **[Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/)** for more information on CIS Benchmarks that have reached end of life.
- Oracle Database 12c

### Security 

- Resolved security vulnerabilities present in embedded, third party dependencies. See our **[knowledge base article](https://cisecurity.atlassian.net/servicedesk/customer/portal/15/article/2658959368)** for more information.

### Application 

- None

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.19.0 
Release Date: Jun 28, 2022 

### Benchmark Coverage 

- Microsoft Windows 10 EMS Gateway v1.1.0
- Microsoft Windows Server 2008 R2 v3.3.0
- Oracle Cloud Infrastructure Container Engine for Kubernetes(OKE) Benchmark v1.1.0
- RedHat OpenShift Container Platform Benchmark v1.2.0

### Security 

- None

### Application 

- Assessment errors causing an exit to the assessment process will now show the exit code as well as the description on the console and logs.
- Centralized assessment errors resolved by removing End of life (EOL) CIS Benchmarks from the Centralized Windows and Linux scripts. 
- The Linux centralized scripts now correctly identify SUSE 15.
- The Linux centralized scripts have been updated to resolve an incorrect reference issue for Oracle Linux.
- To assist in setting remediation priority, HTML reports have been enhanced with a filter for configuration assessment results for recommendations mapped to CIS Critical Security Controls V8 Implementation Group 1 (IG-1). See our upcoming blog to read about how the latest report feature.

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.18.0
Release Date: May 26, 2022 

### Benchmark Coverage 

- Alma Linux 8 v2.0.0
- Kubernetes v1.20 v1.0.1
- Kubernetes v1.23 v1.0.1
- Microsoft Edge v1.0.1
- Microsoft Windows Server 2012 v2.4.0
- Microsoft Windows Server 2012 R2 v2.6.0
- Oracle MySQL Enterprise Edition 8 v1.2.0

The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/#cis-benchmark-coverage) for more information on CIS Benchmarks that have reached end of life.

- Microsoft Windows Server 2003
- Oracle MySQL Community Server 5.6
- Oracle MySQL Enterprise Edition 5.6

### Security 

- The embedded Java in the GUI has been updated to a more recent version.
- Resolved security vulnerabilities present in embedded, third party dependencies. See our **[knowledge base article](https://cisecurity.atlassian.net/l/c/EdN2CSNb)** for more information.

### Application 

- The Advanced Workflow in the GUI when executing a remote Microsoft Windows assessment has been enhanced to assist in selecting the correct port based on selected HTTP or HTTPS communication protocol for WinRM.
- Remote and local assessments will now execute successfully on a MacOS version 12.3 target.
- The HTML report is now consistent with CIS Critical Security Controls V8 nomenclature. Subcontrols are now referred to as Safeguards. Implementation Group abbreviations are capitalized.
- The name of the bundle has been modified to be prefaced with "CIS-CAT". The root directory name has also been modified to "Assessor".

	**NOTE:** If utilizing previous version centralized/batch/shell scripts and configuration files, please note that the names in the file path will now be different.

### Documentation 

- Updated Configuration Guide for Oracle MySQL 8 remote assessment requirements
- Updated Configuration and User Guide for all references and examples to file paths for Assessor to accommodate name change in application and root directory.

---------------------------

## CIS-CAT Pro Assessor, v4.17.0 
Release Date: Apr. 28, 2022 

### Benchmark Coverage 

- Amazon Elastic Kubernetes Service (EKS) v1.1.0
- Cisco IOS 15 v4.1.1 - *Final release
- Cisco IOS 17 v1.0.0
- Fedora 28 Family Linux v2.0.1
- Microsoft Windows Server 2016 v1.4.0
- Microsoft Windows Server 2016 STIG v1.2.0
- Oracle MySQL Community Server 5.6 v2.0.0 - *Final Release
- Oracle MySQL Community Server 5.7 v2.0.0
- Oracle MySQL Enterprise Edition 5.6 v2.0.0 - *Final Release
- Oracle MySQL Enterprise Edition 5.7 v2.0.0

*CIS Benchmarks marked with a "Final release" above will be moved to End of Life in the following CIS-CAT release.

The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/#cis-benchmark-coverage) for more information on CIS Benchmarks that have reached end of life.

- Cisco IOS 12
- Debian 8

### Security 

- None

### Application 

- The GUI now supports configuration assessments with the integrated security property for Microsoft SQL Server.
- CIS Critical Security Controls 8 Implementation Groups shown on HTML report where mappings exist
- Corrected an issue with configuration assessment XML (ARF format) output. It is required to update to the latest assessor version if using CIS-CAT Pro Dashboard and utilizing the HTML export function. Results created on assessor version 4.16.x series cannot be exported via HTML from the Dashboard.

**NOTE:** Release note removed for MacOS v12.3 support. This will be officially delivered in version 4.18.0. Please contact **[support](https://www.cisecurity.org/support/)** if you need an interim development build.

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.16.1 
Release Date: Apr. 4, 2022 

### Benchmark Coverage 

- None

### Security 

- Resolved security vulnerability present in embedded, third party dependency of postgresql. This library was updated to version 42.2.25. See our **[knowledge base article](https://cisecurity.atlassian.net/l/c/w3C5QBPi)** for more information.

### Application 

- None

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.16.0 
Release Date: Mar. 29, 2022 

### Benchmark Coverage 

- Cisco IOS 16*
- Fedora Family Linux 28
- Microsoft Windows Server 2019 v1.3.0
- Microsoft Windows Server 2019 STIG v1.1.0
- MongoDB 5 v1.1.0
- Oracle Linux 8
- Palo Alto Firewall 9 v1.0.1 (offline only)** 
- Palo Alto Firewall 10 v1.0.0 (offline only)**
- Rocky Linux 8

\* Automated assessment content has been modified to more closely align with our consensus process. Please view the change log for the selected Cisco IOS Benchmark. CIS would like to add more automation to the Cisco IOS Benchmark recommendations. Please join our [Cisco Community on CIS WorkBench](https://workbench.cisecurity.org/communities/public) and ask how you can help. 

\** CIS would like to add more automation to the Palo Alto Benchmark recommendations. Please join our Palo Alto [Community on CIS WorkBench](https://workbench.cisecurity.org/communities/public) and ask how you can help.

The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/#cis-benchmark-coverage) for more information on CIS Benchmarks that have reached end of life.

- CentOS Linux 8
- SUSE 11

### Security 

- README.txt file contains information regarding third-party dependency vulnerabilities suppressed by CIS-CAT for various reasons

### Application 

- Non fatal errors for ERROR com.opendxl.client.DxlClient will no longer be displayed on the console
- The Microsoft Windows centralized scripts (cis-cat-centralized.bat and cis-cat-centralized-ccpd.bat) updated to include Microsoft Windows 11 CIS Benchmark
- The Assessor can now properly process datastreams that have had their namespace awareness turned off
- The connection string interactive value for databases and VMWare ESXi now supports use of special characters as a value. CIS-CAT does not support "&" for use in interactive strings for PostgreSQL and Oracle MySQL.
- A new property added to assessor-cli.properties file, validate.xml.schematron, that can be utilized to validate that OVAL definitions for benchmark automated assessment files are formed properly. By default, the property is set to "false". The property, when set to true, will automatically check the benchmark content. This can be useful for validating tailored content.

### Documentation 

- Configuration guide updated to include:
	- Information on automated assessments of Azure Kubernetes Service (AKS)
	- Information on automated assessments of a Palo Alto network device
	- Screen shots of where to place license files
	- Modified information on VMWare ESXi connection string values and now handling of special characters

---------------------------

## CIS-CAT Pro Assessor, v4.15.0 
Release Date: Feb. 25, 2022

### Benchmark Coverage 

- Azure Kubernetes Service (AKS) v1.1.0
- CentOS Linux 8 - Final Release*
- Kubernetes V1.23 v1.0.0
- Microsoft Windows 10 EMS Gateway v1.0.0
- Microsoft Windows 10 v1.12.0
- Microsoft Windows 11 v1.0.0
- Microsoft Windows Server 2022 v1.0.0
- Red Hat Enterprise Linux 8 v2.0.0
- SUSE Linux Enterprise 11 v2.1.1 - Final release*

\* CIS Benchmarks marked with a "Final release" above will be moved to End of Life in the following CIS-CAT release.

### Security 

- None

### Application 

- None

### Documentation 

- None 

---------------------------

## CIS-CAT Pro Assessor, v4.14.0 
Release Date: Jan. 26, 2022 

### Benchmark Coverage 

- SUSE Linux Enterprise 12 v3.1.0
- SUSE Linux Enterprise 15 v1.1.1

Lite now includes Ubuntu 20.04

### Security 

- Resolved security vulnerability present in embedded, third party dependencies:
	- OpenDXL Java Client, which includes log4j. This library is now a derivative work of version 0.2.6 which includes log4j 2.17.1. to resolve CVE-2021-44832 (medium CVSS)
	- For logback-core and logback-classic.These libraries have been moved to version 1.2.10.

### Application 

- Automated assessment content where no profile exists now successfully executes.
- When performing a configuration assessment with some datastream content containing external links will no longer receive an error.
- The GUI now supports use of special characters (<,>, &,", ') within interactive values such as passwords for Database / ESXi connection strings.
- Linux remote assessments will now support additional machines where the installed SSH components utilize stronger encryption algorithms.
- GUI warning and removal of non-existent Benchmark from loaded configuration file when referenced BM does not exist in the Benchmark folder.
-  GUI warning and option to replace a prior version Benchmark from loaded configuration file when referenced BM version does not match the version in the Benchmark folder.

### Documentation 

- None 

---------------------------

## CIS-CAT Pro Assessor, v4.13.1 
Release Date: Dec. 20, 2021 

### Benchmark Coverage 

- None

### Security 

- Resolved security vulnerability present in embedded, third party dependency of log4j-core. This library was updated to version 2.17.0. See our **[knowledge base article](https://cisecurity.atlassian.net/l/c/P1VQ0bYo)** for more information.

### Application 

- None

### Documentation 

- None 

---------------------------

## CIS-CAT Pro Assessor, v4.13.0 
Release Date: Dec. 14, 2021 

### Benchmark Coverage 

- Apple macOS 12.0 Monterey v1.0.0
- Google Chrome v2.1.0

The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/#cis-benchmark-coverage) for more information on CIS Benchmarks that have reached end of life.

- Mac OS 10.14
    
### Security 

- Resolved security vulnerability present in embedded, third party dependency of log4j-core. This library was updated to version 2.15.0. See our **[knowledge base article](https://cisecurity.atlassian.net/l/c/P1VQ0bYo)** for more information.

### Application 

- Update to Powershell library to increase connectivity success as well as performance for VMWare ESXi
- Update to WinRM library to allow secure HTTP connection, which provides an option to reduce complexity of WinRM preparation on target endpoint
-  VMWare ESXi connections more successful when encountering passwords with special characters.
-  The "Basic" workflow in the GUI application will no longer encounter an error when the local machine names begins with a number. The schema has not changed, but the Basic GUI workflow will now always generate a compliant ID.
-  Improved accuracy, performance and error handling for VMWare ESXi when USB device settings were present

### Documentation 

- Configuration Guide updated in VMWare ESXi section to specify assessments are supported on a Microsoft Windows operating system only.
- Updated configuration guide for Windows remote endpoint configuration to reflect the benefits of the updated WinRM library 

---------------------------

## CIS-CAT Pro Assessor, v4.12.0 
Release Date: Nov. 18, 2021 

### Benchmark Coverage 

- Amazon Linux 2 STIG v2.0.0
- Apple macOS 10.14 v2.0.0 - Final release *
- Apple macOS 10.15 Catalina v2.0.0
- Apple macOS 11.0 Big Sur v2.0.0
- Google Kubernetes Engine (GKE) v1.2.0
- MongoDB 3.6 v1.1.0 **
- PostgreSQL 14 v1.0.0 **
- Red Hat Enterprise Linux 7 STIG v2.0.0
- Red Hat Enterprise Linux 8 STIG v1.0.0

The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/#cis-benchmark-coverage) for more information on CIS Benchmarks that have reached end of life.

- Apple OSX 10.12
- Mac OS 10.13
    
\* CIS Benchmarks marked with a "Final release" above will be moved to End of Life in the following CIS-CAT release.

\** Not applicable to CIS-CAT Pro Assessor v4 Service

### Application 

- None

### Security 

- Resolved security vulnerabilities present in embedded, third party dependency of bcprov-jdk15on. This library was moved to version 1.69.

### Documentation 

- Configuration guide updated to include information on Google Kubernetes Engine (GKE)
- Updated configuration guide to expand on the use of the interactive value for Mongo DB.
- Updated User Guide Assessor in the Benchmark/Data-Stream Collection Options specifically for the -b option to mention when utilizing a Benchmark with a parenthesis character in the name that it must be enclosed in quotes.

---------------------------

## CIS-CAT Pro Assessor, v4.11.0 
Release Date: Oct. 28, 2021

### Benchmark Coverage 

- AlmaLinux OS 8 v1.0.0
- MongoDB 5 v1.0.0
- SCE scripts, required for accurate assessment results, supporting Linux/Unix Benchmarks updated.
    
### Application 

- Non-English characters are handled and no longer result in an exception when encountered during some assessments (primarily Microsoft Windows).
- Linux assessment processes improved to now handle file path spaces, when encountered.

### Security 

- Improved security measures applied to validate the CIS-CAT Assessor code integrity.

### Documentation 
- Configuration guide updated in Microsoft Windows section that addresses setting up WinRM with Group Policy. Setting up WinRM via local policy is possible, but CIS Microsoft Windows Benchmarks are designed for domain-joined machines.

---------------------------

## CIS-CAT Pro Assessor, v4.10.0 
Release Date: Sep. 29, 2021 

### Benchmark Coverage 

- Microsoft Windows Server 2012 v2.3.0
- Microsoft Windows Server 2012 R2 v2.5.0
- Microsoft Windows Server 2016 STIG v1.1.0
- SUSE Linux 15 v1.1.0
- VMWare ESXi 6.7 v1.2.0
    
### Application 

- MacOS assessment results are now more accurate for recommendations that check conditions for profiles (plist).
- The GUI application has upgraded to a more current version of the baseline software.

### Security 

- None 

### Documentation 

- Additional information added to VMWare ESXi in configuration guide on valid connection string values. 
- Configuration Guide updated to include more information on how a Member's license key is validated.

---------------------------

## CIS-CAT Pro Assessor, v4.9.0 
Release Date: Aug 31, 2021 

### Benchmark Coverage 

- CentOS Linux 7 v3.1.2
- MongoDB 4 v1.0.0
- VMWare ESXi 7 v1.1.0
    
### Application 

- None

### Security 

- None 

### Documentation 
- The TNS Listener interactive value for Oracle 12c, 18c, and 19c defined in Configuration Guide in the Database section.
- More clarification on supported operating systems for database assessments added to Configuration Guide. Specifically do not support Solaris-hosted databases.

---------------------------

## CIS-CAT Pro Assessor, v4.8.2 
Release Date: Aug 9, 2021

### Benchmark Coverage 

- None

### Application 

- None

### Security 

- Resolved security vulnerabilities present in embedded, third party dependencies. 
	- Please see the related [knowledge base article](https://cisecurity.atlassian.net/servicedesk/customer/portal/15/article/2237857936) for more information 

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.8.0 
Release Date: July 27, 2021

### Benchmark Coverage 

All Benchmarks released to CIS-CAT this version and after will contain Controls 8 annotations.  Controls 6 mappings are deprecated and will no longer appear on the report.

- Amazon Linux 2 v2.0.0
- Microsoft Windows 10 21H1 v1.11.0
- Microsoft Windows Server 2016 v1.3.0
- Oracle MySQL Enterprise Edition 8.0 v1.1.0
- Ubuntu Linux 20.04 LTS STIG v1.0.0

### CIS-CAT Pro Updates 

- Corrected an error where SCE scripts to support Linux assessments were not properly collected when an absolute path of assessor was used.

### Documentation 

- Updated deployment guide to contain more information on Java requirements.

---------------------------

## CIS-CAT Pro Assessor, v4.7.0 
Release Date: May 27, 2021 

### Benchmark Coverage 

All Benchmarks released to CIS-CAT this version and after will contain Controls 8 annotations.  Controls 6 mappings are deprecated and will no longer appear on the report.
Only the latest Microsoft Windows 10 Benchmark will be included. See the Coverage Guide for more information.

- Apple macOS 10.14 v1.4.0 
- Apple macOS 10.15 v1.4.0 
- Apple macOS 11.0 v1.2.0 
- CentOS Linux 7 v3.1.1
- CentOS Linux 8 v1.0.1
- Debian Linux 8 v2.0.2 - Final Release
- Kubernetes v1.20 Benchmark v1.0.0
- Microsoft Intune v1.0.1
- Microsoft Windows Server 2019 v1.2.1
- Microsoft Windows Server 2019 STIG v1.0.1
- Microsoft Windows 10 20H2 v1.10.1
- Oracle Linux 7 v3.1.1
- Oracle Linux 8 v1.0.1
- Red Hat Linux 7 v3.1.1
- Red Hat Linux 8 v1.0.1

### CIS-CAT Pro Updates 

- Windows assessment errors resolved when user group setup contain circular references.
- Update to third-party library mariadb-java-client to latest version, 2.7.2.
- HTML configuration assessment reports now support CIS Benchmark Control 8 mapping. New and updated Benchmarks released in V4.7.0+ will be mapped to Controls 8 released May 18, 2021.
- Windows centralized scripts updated to utilize the just the latest Windows 10 Benchmark for Windows 10 platforms.

### Documentation 

- Updated configuration assessment guidance for Kubernetes Benchmark.

---------------------------

## CIS-CAT Pro Assessor, v4.6.0 
Release Date: April 29, 2021

### Benchmark Coverage 

- CentOS Linux 7 v3.1.0
- Microsoft SQL Server 2016 Benchmark v1.3.0 (*new driver format for V4 ONLY)
- Microsoft SQL Server 2017 Benchmark v1.2.0 (*new driver format for V4 ONLY)
- Microsoft SQL Server 2019 Benchmark v1.2.0 (*new driver format for V4 ONLY)
- Microsoft Windows Server 2019 Benchmark v1.2.0
- Microsoft Windows Server 2019 STIG Benchmark v1.0.0
- Oracle Linux 7 Benchmark v3.1.0
- Red Hat Enterprise Linux 7 Benchmark v3.1.0
- Red Hat Enterprise Linux 7 STIG Benchmark v1.0.1
- SUSE Linux Enterprise Server 12 Benchmark v3.0.0
- Ubuntu Linux 20.04 LTS Benchmark v1.1.0
- VMware ESXi 7.0 Benchmark v1.0.0

\* Please be aware that the Microsoft SQL Server driver has changed with this release. See the [database section in the Configuration Guide](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#database-assessment) on the new format needed for CIS-CAT Pro Assessor v4.6.0+. Prior versions of CIS-CAT and v3 continue to use the previous connection url format.

### CIS-CAT Pro Updates 

- Database assessment output (reports and dashboard imports) are now identified by each database instead of the host machine of the database.
- Configuration assessments will continue with an "unknown" database name when this value is not set instead of producing an error.
- Better handling of certain characters causing errors in Windows assessments.
- A VMWare ESXi hostname will now accurately display on the HTML cover page and preface a results filename.
- A new jdbc driver added to support Microsoft SQL Server database assessments. NOTE: New driver requires a connection string format change indicated in the [Configuration ](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#database-assessment) and [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/#cis-benchmark-coverage).

### Documentation 

- Configuration Guide updated in Database section to include summary of Interactive Values needed for Database assessments. Updated Microsoft SQL Server information for new URL connection string format and links to updated driver properties.

---------------------------

## CIS-CAT Pro Assessor, v4.5.0 
Release Date: March 30, 2021 

### Benchmark Coverage 

- Apple macOS 10.14 v1.3.0
- Apple macOS 10.15 v1.3.0
- Apple macOS 11.0 v1.1.0
- Cisco IOS 15 v4.1.0
- Cisco IOS 16 v1.1.1
- PostgreSQL 13 v1.0.0
- RedHat OpenShift Container Platform v4 Benchmark v1.1.0
- Ubuntu 16.04 v2.0.0
- Ubuntu 18.04 v2.1.0

### CIS-CAT Pro Updates 

- Incorporated new PowerShell library to improve performance of local Microsoft Windows/VMWare assessments. This will resolve issues where Windows and VMWare assessments experienced excessive wait time.
- Resolved an error with benchmark signature validation when the assessed system is configured with FIPS enabled.

### Documentation 

- Updated the Configuration Guide to include information about the new Red Hat OpenShift  Container CIS Benchmark.

---------------------------

## CIS-CAT Pro Assessor, v4.4.0 
Release Date: February 25, 2021 

### Benchmark Coverage 

- CentOS Linux 6 v3.0.0
- Microsoft Windows 10 Enterprise Release 20H2 v1.10.0
- Oracle Linux 6 v2.0.0
- Red Hat Linux 6 v3.0.0

### CIS-CAT Pro Updates 

- Resolved an issue with assessing with datastream content where evaluation of SCE script content would result in 'unknown' results.
- A '~' character was removed from line 39 of the assessor-cli.sh as it caused errors when run in bash in automation frameworks.

### Documentation 

- Note VMWare ESXi and Windows System configuration should not configure LanguageMode to ConstrainedLanguage as assessment execution will be blocked.
- Clarified that JRE 11 is required for assessing Microsoft SQL Databases that utilize SSL properties in the connection string such as IntegratedSecurity.

---------------------------

## CIS-CAT Pro Assessor, v4.3.1 
Release Date: January 28, 2021

### Benchmark Coverage 

- None

### CIS-CAT Pro Updates 

- Configuration files containing the deprecated `<starting_dir>` element will no longer receive a parsing error. Assessor will ignore the element and allow the file to load in the GUI and CLI operations to continue.

### Documentation 

- None

---------------------------

## CIS-CAT Pro Assessor, v4.3.0 
Release Date: January 26, 2021

### Benchmark Coverage 

- None

### CIS-CAT Pro Updates 

- The GUI Advanced Workflow for remote assessments now allows use of domain usernames where "@" is utilized (username = user@domain). The configuration XML schema has been updated to support this change.
- The default temporary location utilized during remote Linux assessments has changed from /tmp to a temporary location within the user's home directory. Better console messaging and logging information has been added when a temporary location is invalid.
- The `<starting_dir>` option is no longer used in the configuration XML or on the command line with -d. Use absolute path of assessor-cli.bat or .sh when not executing in the root assessor location.
- Resolved an issue where CIS tailored Benchmarks with certain names would prevent all benchmarks from loading to the v4 GUI selection screen.
- Microsoft Windows vulnerability assessment results are more accurate as file versions are now evaluated using a more reliable method.
- Execution of assessor-cli.bat or .sh can now occur from any directory on the command line when the absolute path is provided to the desired assessor directory.
- Cisco IOS assessment reports will now consistently import to the Dashboard without error.
- An error was corrected when scanning Cisco IOS using the GUI.

### Documentation 

- Updated User Guide with more information on Assessment Results displayed in the Console and clarified information on report scoring.
- Update to VMWare ESXi requirements that enabling ssh is not required.
- Update to Microsoft SQL Server Database section to indicate configuration assessment process can support dynamic port configuration for a local scan.

---------------------------

## CIS-CAT Pro Assessor, v4.2.0 
Release Date: December 17, 2020 

### Benchmark Coverage 

- Apache Tomcat 9 v1.1.0
- Oracle Database 19c v1.0.0
- Red Hat Enterprise Linux 5 has moved to end of life and is no longer officially supported. See the Coverage Guide for more information on end of life CIS Benchmarks.

### CIS-CAT Pro Updates 

- Remote Linux assessment results are now more accurate when executed by "root" user. Please note that CIS Benchmark recommends authenticating as sudo for access over SSH.
- New property allows option to hide timestamp from generated output reports.
- Configuration assessment checks depending on a variable value that doesn't exist will no longer provide inaccurate results.
- A JSON version of the configuration assessment report is now available from the command line. 

### Documentation 

- Update to documentation to indicate that v4 GUI cannot initialize from a network location.
- Updated User Guide for new JSON report format command line option.
- Remote assessment for CIS Kubernetes Benchmark clarified in the Configuration Guide.
- A new section entitled "Apache Tomcat 9 Assessment" has been added to the Configuration Guide to provide guidance for this new Benchmark.

---------------------------

## CIS-CAT Pro Assessor, v4.1.0 
Release Date: November 19, 2020 

Read our [blog](https://www.cisecurity.org/blog/the-evolution-of-cis-cat-and-a-new-gui-in-cis-cat-v4-1-0/) on this release.

### Benchmark Coverage 

- MacOS 10.13 v1.1.0
- MacOS 10.14 v1.1.0
- MacOS 10.15 v1.1.0
- Microsoft Edge v1.0.0
- Microsoft Windows 10 Enterprise Release 2004 v1.9.1

### CIS-CAT Pro Updates 

- The python.log is no longer created.
- CIS-CAT Pro v4 Assessor v4.1.0 and Assessor v4 Service v1.1.0 versioning has incrementally changed to mark the introduction of licensing and addition of a GUI.
- Assessor v4.1.0+ and v4 Service v1.1.0+ now require a license key for full functionality and CIS Benchmark availability.
- All manual recommendations now show on csv, HTML, and text configuration reports. "Manual" recommendations will continue to be excluded from the overall score of the report since the score can only be calculated by considering the fully-automated recommendations. See our [blog](https://www.cisecurity.org/blog/changes-to-cis-benchmark-assessment-recommendation-scoring/).

	**NOTE: For full tool features, download license key files from CIS WorkBench and place in License folder. This location can be modified, if desired, in the assessor properties files. See the [License](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/#license) section in the configuration guide for full instructions.**

### Documentation 

- VMware configuration documentation updated to mention CIS Benchmark recommendation consideration for ssh enablement.
- The assessor-cli.properties file corrected to show the proper value name example for Microsoft SQL Server interactive value.

---------------------------

## CIS-CAT Pro Assessor, v4.0.24 
Release Date: October 1, 2020 

### Benchmark Coverage 

- Amazon Elastic Kubernetes Service (EKS) 1.0.1
- Kubernetes v1.6.1
- Microsoft Windows Server 2016 STIG v1.0.0
- Red Hat Linux 7 v3.0.1. Resolves excessive duration assessment process when attached user home drives exist.

### CIS-CAT Pro Updates 

- VMWare ESXi assessments for certain configurations now complete without error.
- Updated Linux SCE scripts to enable more accurate Linux configuration assessment results where recommendations check IPV6 states.
- The temporary folder will no longer increase in size in some circumstances when an error is encountered during an assessment.
- The assessor configuration file, used in remote assessments, now supports additional reporting option output for JSON. This option previously was only available on the command line.
- The "license" folder within CIS-CAT Pro bundle renamed to be more descriptive of the content to third_party_licenses.
- Readme file updated to show new CIS Support portal information.
- Linux centralized scripts updated to include latest CIS benchmark versions for CentOS 7, Red Hat 7, and Oracle Linux 7.
- Corrected an issue in the ARF where "notapplicable" was being written to the result instead of "not applicable".
- Configuration xml files now support one or multiple Cisco IOS tech files for assessment.

### Documentation 

- Examples added for assessing with VMWare ESXi 6.7 Benchmark.
- Additional information provided for executing a configuration assessment with a CIS Kubernetes Benchmark.

---------------------------

## CIS-CAT Pro Assessor, v4.0.23 
Release Date: August 25, 2020 

### Benchmark Coverage 

- Debian Family Linux v1.0.0
- Fedora 19 Family v1.0.0
- Microsoft Windows 10 Enterprise Release 2004 v1.9.0
- The following CIS Benchmarks have moved to end of life and are no longer officially supported. See the [Coverage Guide](https://ccpa-docs.readthedocs.io/en/latest/Coverage%20Guide/) for more information.
	- Microsoft SQL Server 2008 R2
	- Microsoft SQL Server 2012
	- Microsoft SQL Server 2014

### CIS-CAT Pro Updates 

- Resolved an issue with configuration results for MacOS for the Gatekeeper recommendation 2.6.2 check.

### Documentation 

- Updated Linux centralized assessment workflow. Renamed "Assessing Multiple Windows and Linux" sections of the Configuration Guide to be prefaced with "Centralized".

---------------------------

## CIS-CAT Pro Assessor, v4.0.22 
Release Date: July 30, 2020 

### Benchmark Coverage 

- Microsoft SQL Server 2008 R2 v1.7.0 - Final release *
- Microsoft SQL Server 2012 v1.6.0 - Final release *
- Microsoft SQL Server 2014 v1.5.0 - Final release *
- Microsoft SQL Server 2016 v1.2.0
- Microsoft SQL Server 2017 v1.1.0
- Microsoft SQL Server 2019 v1.1.0
- Oracle 18c v1.0.0
- SUSE Linux 15 Enterprise v1.0.0
- Ubuntu Linux 20.04 v1.0.0

### CIS-CAT Pro Updates 

- Added support for Java versions 8.251 through 14. Imports to Dashboard will now be successful when imported via the API.
- Errors will no longer occur if the default sessions.properties file is removed or renamed.
- Resolved an error with vulnerability HTML report generation.
- SuSE 15 and Ubuntu 20.04 now supported for vulnerability assessments.
- Target system state resulting in a score of "Fail" on a configuration assessment HTML assessment report are now emphasized with color and text.
- The link to initiate a support request that appears on an HTML report has changed to URL location where Members can enter support issues cisecurity.org\support.
- Resolved an error with Windows 10 vulnerability assessments.
- Ubuntu vulnerability definitions are now saved in assessor folder in an unzipped format and ready for use. 

### Documentation 

- Corrected steps for CIS Host Server setup in "Assessing Multiple Unix/Linux Targets" section.
- Third party license version number information maintained in license.file relevant to each release of CIS-CAT Pro Assessor v4.

\* CIS Benchmarks marked with a "Final release" above will be moved to End of Life in the following CIS-CAT release.

---------------------------

## CIS-CAT Pro Assessor, v4.0.21 
Release Date: June 30, 2020 

### Benchmark Coverage 

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

### CIS-CAT Pro Updates 

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

### Documentation 

- Information on interpreting the HTML configuration report included in the guide. 

---------------------------

## CIS-CAT Pro Assessor, v4.0.20 
Release Date: May 5, 2020 

### Benchmark Coverage 

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

### CIS-CAT Pro Updates 

- Assessor can now collect and interpret system registry values while assessing Windows target systems when values contain non-English characters.
- Due to EOL of Canonical's Ubuntu 12, CIS-CAT no longer officially supports vulnerability assessments for this version of the operating system.
- A new property (esxi.max.wait) allows configuration of the maximum timeout value for the execution of each machine state collection command during a VMWare assessment.
- A deprecated property, user.assigned.machine.name property, was removed from the assessor-cli.property file.
- Updated to include the latest JSON 1.1 vulnerability feed data.

### Documentation 

- Step-by-step instructions for Windows Task scheduling removed and replaced with more generic guidance with the understanding that Members have multiple different environments.
- Modified "Configuration Guide" to be more specific about preferred versions of Java to utilize with CIS-CAT Pro.
- Additional information now available on property settings.

---------------------------

## CIS-CAT Pro Assessor, v4.0.19 
Release Date: March 25, 2020

### Benchmark Coverage 

- None

### CIS-CAT Pro Updates 

- Corrected an error in the display of the header in csv-formatted assessment results.
- Corrected the display of the CCE ID field in csv-formatted assessment results.
- Resolved an error when assessing Microsoft Windows Server 2008 R2.
- When downloading the latest, supported vulnerability definitions using CIS-CAT Pro commands, Microsoft Windows Server 2019 will now be included. SuSe Linux definition collection has also been updated.
- Using the -npr option on the command line, configuration assessment results can be produced in json format.
- Default Java memory allocation increased to 2 GB (2048MB) in all assessor-cli.bat and .sh and centralized scripts. This will require 64 bit Java installation. When running 32 bit Java, the scripts will need to be updated to 1024 MB. The Documentation now includes recommendations to set WinRM memory allocation and verify the current setting on target systems.
- Assessor will no longer incur an error when a detected file is subsequently deleted during an assessment of a textfilecontent54_test OVAL test.
- Updated to include the latest JSON 1.1 vulnerability feed data.

### Documentation 

- Default options available for configuration in the assessor-cli.properties file are now described in further detail in the online documentation. See the "Properties" section of the Configuration Guide.

---------------------------

## CIS-CAT Pro Assessor, v4.0.18 
Release Date: February 25, 2020

### Benchmark Coverage 

- CIS Debian Linux 10 Benchmark v1.0.0
- CIS Kubernetes Benchmark v 1.5.1
- CIS Microsoft SQL Server 2019 Benchmark v1.0.0
- CIS Microsoft Windows 10 Enterprise 1903 v1.7.1
- CIS Microsoft Windows 10 Enterprise 1909 v1.8.1
- CIS MongoDB 3.6 v1.0.0

### CIS-CAT Pro Updates 

- Remote Window sessions can now successfully connect for an assessment when using versions of Java 9 and above. A "javax" exception will no longer occur.
- Remote Microsoft SQL database assessments will no longer end in error when executed from operating systems other than Microsoft where PowerShell was installed instead of default.
- Enhanced Linux assessment process to handle some large system values encountered.
- Assessments of Microsoft SQL databases will have improved connection success as additional environment analysis has been added to the process.
- Database JDBC connection strings now obfuscated in log files.
- An error was resolved for Cisco remote assessments.
- Updated to include the latest JSON 1.1 vulnerability feed data.

### Documentation 

- Updated Windows endpoint remote configuration for WinRM in flowchart and IPv4 and IPv6 filter settings.
- Linux assessments where user home directories exist on an auto-mounted, large storage drive, will experience longer assessment duration as some benchmarks check will take longer to complete.

---------------------------

## CIS-CAT Pro Assessor, v4.0.17 
Release Date: January 29, 2020

### Benchmark Coverage 

- CIS Debian Linux 9 Benchmark v1.0.1
- CIS Fedora 28 Family Linux v1.0.0, intended for any Divertive Distribution of Linux.  Requires the "ignore.platform.mismatch" property be set to "true" in the Assessor's properties file.
- CIS Microsoft Windows Server 2019 Benchmark v1.1.0
- CIS Ubuntu Linux 18.04 v2.0.1

### CIS-CAT Pro Updates 

- Updated to include the latest JSON 1.1 vulnerability feed data.

---------------------------

## CIS-CAT Pro Assessor, v4.0.16 
Release Date: January 15, 2020

### Benchmark Coverage 

- Microsoft Windows 10 Enterprise 1909 v1.8.0
- Microsoft Windows 10 Enterprise 1903 v1.7.0

### CIS-CAT Pro Updates 

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

---------------------------

## CIS-CAT Pro Assessor, v4.0.15 
Release Date: December 19, 2019 

### Benchmark Coverage 

- None

### CIS-CAT Pro Updates 

- Linux assessments have been corrected with updated SCE scripts. Previous scripts inadvertently contained characters causing "unknown" results for some recommendations.

---------------------------

## CIS-CAT Pro Assessor, v4.0.14 
Release Date: December 18, 2019 

### Benchmark Coverage

- Controls Assessment Module - Implementation Group 1 for Microsoft Windows Server 2016 v1.0.0

### CIS-CAT Pro Updates

- Enhanced Linux assessment process accommodates large user IDs.
- Controls Assessment Module file name change to identify Microsoft Windows 10 v1.0.3.
- Updated to include the latest JSON 1.1 vulnerability feed data.

---------------------------

## CIS-CAT Pro Assessor, v4.0.13 
Release Date: December 4, 2019

### Benchmark Coverage 

- CIS CentOS Linux 8 Benchmark v1.0.0
- CIS Microsoft Windows 10 Enterprise Release 1809 Benchmark v1.6.1
- CIS Microsoft Windows Server 2019 Benchmark v1.0.1
- CIS Oracle Linux 8 Benchmark v1.0.0
- CIS Red Hat Enterprise Linux 8 Benchmark v1.0.0

### CIS-CAT Pro Updates 

- Benchmarks are now sorted alphabetically when viewed on Linux CLI in interactive mode (using option -i).
- Linux assessments results for recommendation 5.3.4 are now accurate. 
- Updated to include the latest JSON 1.1 vulnerability feed data.

---------------------------

## CIS-CAT Pro Assessor, v4.0.12 
Release Date: October 31, 2019 

### Benchmark Coverage 

- Alibaba Cloud Aliyun Linux 2 v1.0.0

### CIS-CAT Pro Updates 

- An option maintained in the properties file has been added to compress assessment result files prior to automatic import to CIS-CAT Pro Dashboard v1.1.9+ via API.
- Benchmark version number is now displayed when using the command line in interactive mode.
- ARF XML and HTML report generation issue resolved for Windows 10 1803 remote assessments.
- Cisco IOS target system correct domain or IP is now correctly shown on the HTML and ARF XML.

**IMPORTANT:** To utilize the new option to compress assessment results on post to Dashboard, users must upgrade to CIS-CAT Pro Dashboard v1.1.9. See the assessor-cli.properties file for more information.

---------------------------

## CIS-CAT Pro Assessor, v4.0.11 
Release Date: September 25, 2019

### Benchmark Coverage 

- CIS Microsoft Windows Server 2019 v1.0.0
- CIS MS Windows 10 Enterprise 1809 v1.6.0

### CIS-CAT Pro Updates 

- Updated to include the latest JSON 1.1 vulnerability feed data.

---------------------------

## CIS-CAT Pro Assessor, v4.0.10 
Release Date: August 27, 2019

### Benchmark Coverage 

- None

### CIS-CAT Pro Updates 

- MS Windows 10 configuration assessment HTML report displays OVAL assessment collected system values, recommended Benchmark values and rule used to generate pass/fail result.
- Support for NIST vulnerability JSON data feeds.
- Additional enhancements Ubuntu 18.04 assessment process to ensure more accurate results.
- Major performance improvements (10-100% performance increase) for Linux assessment process, particularly where a target has an attached a mounted file system. Additional option to exclude mounted file system, when necessary, for Linux only.
- Updated to latest NVD CVE feeds for up-to-date display of CVE information, including CVSS base scores and vector strings in HTML Reports.

---------------------------

## CIS-CAT Pro Assessor, v4.0.9 
Release Date: July 25, 2019 

### Benchmark Coverage 

- PostgreSQL 11 v1.0.0
- Debian Linux v2.0.1

### CIS-CAT Pro Updates 

- Updated to latest NVD CVE feeds for up-to-date display of CVE information, including CVSS base scores and vector strings in HTML Reports.  This update includes the 2019 feed.
- CIS-CAT Pro Assessor v4 vulnerability reports for Windows Server 2008 R2 can now import successfully into CIS-CAT Pro Dashboard.

---------------------------

## CIS-CAT Pro Assessor, v4.0.8 
Release Date: June 28, 2019 

### Benchmark Coverage 

- None

### CIS-CAT Pro Updates 

- Cisco IOS configuration assessment process enhanced to accommodate additional configuration scenarios
- Enhanced Ubuntu 18.04 configuration process to ensure more accurate results
- The unix/linux centralized scripts have been corrected to refer to the proper CIS-CAT Pro Assessor jar file
- Correction to linux centralized script for Debian operating systems
- Linux centralized scripts can now be used to assess Mac OS 10.13
- CIS-CAT Pro Assessor v4 vulnerability reports for Windows Server 2012 can now import successfully into CIS-CAT Pro Dashboard
- New section added to Controls Assessment Module documentation to provide information on remediation steps for automated checks
- Debian operating systems are now properly detected and assessed on local assessments and when pairing with external application build scripts

---------------------------

## CIS-CAT Pro Assessor, v4.0.7 
Release Date: June 3, 2019

### Benchmark Coverage 

- Debian Linux 8 Benchmark v2.0.0.1

### CIS-CAT Pro Updates 

-  Error corrected for local Linux/Unix/Mac OS configuration assessments. Results will now be accurate for recommendations referring to files or file directories.

---------------------------

## CIS-CAT Pro Assessor, v4.0.6 
Release Date: May 29, 2019 

### Benchmark Coverage 

- PostgreSQL 10 v1.0.0
- NGINX v1.0.0
- Mac OS 10.13 with OVAL support
- Google Chrome v75 v2.0.0
- MS SQL Server 2017 v1.0.0
- MS SQL Server 2016 v1.1.0
- MS SQL Server 2014 v1.4.0
- MS SQL Server 2012 Benchmark v1.5.0

### CIS-CAT Pro Updates 

-  Consumers can now try V4 command line application with 3 Benchmarks (Ubuntu, Windows 10 Enterprise, Chrome) by downloading V4 Lite. Users can assess endpoints using Controls Assessment Module for Windows 10 Enterprise Implementation Group 1 for Controls V7.1.
-  Enhanced Debian 8 assessment process now produces accurate results for recommendations 1.5.1, 1.5.3, 3.1.1, 3.1.2 and 3.2.1 to 3.2.9.
-  Enhanced Ubuntu Linux assessment process accommodates large system group IDs.
-  Pass/fail assessment results for Windows 10 1803 now include the OVAL evidence.
-  Assess a Windows 10 endpoint with the Controls Assessment Module for Controls 7.1 Implementation Group 1.
-  Assessment result default file descriptions now only include "ARF" on XML configuration files.
-  Enhanced Debian 8 assessment process now produces more accurate results for recommendations 5.1.2 to 5.1.7.

---------------------------

## CIS-CAT Pro Assessor, v4.0.5 
Release Date: April 30, 2019 

### New Benchmarks 

- None

### Benchmark Updates 

- CIS Microsoft Windows 10 Enterprise 1803 v1.5.0.1 - scoring modification only for profile selection of ‘Windows 10 1803 Level 1 (L1) + BitLocker (BL) + Next Generation Windows Security (NG)’ or 'Windows 10 1803 Level 1 (L1) + BitLocker (BL)'

### CIS-CAT Pro Updates 

-  Cisco IOS assessments will now produce accurate results when performing local and remote assessments.
-  Number only credentials for endpoints utilized in the configuration xml files are now valid.
-  A broader explanation and more generic referral to Level 1 Windows Benchmark recommendations that require consideration when remote scanning has been added to the online documentation. In order to remotely scan, users may need to except 2 or more recommendations.
-  Online documentation has been revised for Windows Endpoint Configuration to be more specific to users' environments.

---------------------------

## CIS-CAT Pro Assessor, v4.0.4 
Release Date: March 20, 2019

### New Benchmarks 

- CIS MS Windows 10 Enterprise Release 1803 Benchmark v1.5.0. Updates to centralized scripts and dissolvable bundle to accommodate the new Benchmark. CIS-CAT Pro will support the latest three published Windows Enterprise Benchmarks.
- CIS PostgreSQL 9.6 v1.0.0

### Benchmark Updates 

- CIS Amazon Linux 2 v1.0.0.1 with updated Controls 7 mapping only
- CIS Microsoft IIS 10 Benchmark v1.1.1
- CIS PostgreSQL 9.5 v1.1.0.1

### CIS-CAT Pro Updates 

-  Configuration XML files and sessions.properties files used to drive the assessment process can be encrypted.  See the **"File Encryption Options"** section of the User's Guide for more information.
-  Scripts are included for Linux and Windows environments to scan an entire domain when target machines have access to a network Java instance and CIS-CAT Pro Assessor. This is useful for members who want to use the assessor within a domain instead of remotely connecting to each target. See the **"Assessing Multiple Windows Targets"** and **"Assessing Multiple Unix/Linux Targets"** sections of the User's Guide for more information.
-  On screen message for local assessments will let users know if they lack privileges to execute the assessment.
-  The connection to remote endpoints has been modified to be more efficient.
-  Enhanced documentation with information on allowed characters used within the configuration XML file.
-  Linux configuration results have been corrected for reported issues on Linux CentOS recommendation 6.2.6.

---------------------------

## CIS-CAT Pro Assessor, v4.0.3 
Release Date: January 17, 2019 

### New Benchmarks 

- CIS Debian Linux 9 Benchmark v1.0.0

### Benchmark Updates 

- CIS Debian Linux 8 Benchmark v2.0.0
- CIS Microsoft IIS 10 Benchamrk v1.1.0
- CIS PostgreSQL 9.5 Benchmark v1.1.0

### CIS-CAT Pro Updates 

-  Assessment result HTML reports now show the CIS Controls and CIS Sub-control version numbers when mapped to a CIS Benchmark recommendation. The CIS Control version is only available on some Benchmarks. Check the CIS website for more information. The title page of the report has also been enhanced to display long Benchmark names.
-  Scripts have been modified to allow an assessment to execute with OpenJDK, Java 9, Java 10, and Java 11.
-  User's Guide updated in section titled "Using CIS-CAT Pro Assessor CLI" to highlight requirement for a the user executing the application to have root, Administrator, or an equivalently privileged principal.
-  CIS-CAT Pro assessor has been enhanced to more efficiently work with OVAL content that uses XPath.
-  CIS Microsoft IIS 10 Benchmark has been corrected to properly collect assessment information. In prior versions, some users may have experienced false failures.
-  An issue was resolved with interactive values when users configured private keys with passphrases. The command line will now prompt users to enter a passphrase when the passphrase element is present and null in the Sessions or Config file. If the passphrase element does not exist for a target in the sessions or configuration xml, the command line will not prompt the user for an entry.
-  Report generation errors have been resolved for all versions of CIS Apple OSX 10.10, 10.11 and 10.12 Benchmark.    

---------------------------

## CIS-CAT Pro Assessor, v4.0.2 
Release Date: November 28, 2018 

### New Benchmarks 

- None

### Benchmark Updates 

- None

### CIS-CAT Pro Updates 

-  Resolved User_object NPE/fatal error that occurs during some assessments.
-  Assessment results produced in csv format will now be modified per options set using the -D option.

---------------------------

## CIS-CAT Pro Assessor, v4.0.1 
Release Date: November 21, 2018

### New Benchmarks 

- CIS Amazon Linux 2 Benchmark v1.0.0

### Benchmark Updates 

- CIS Benchmark for Windows Server 2016, v1.1.0

### CIS-CAT Pro Updates 

-  Assessor-CLI.sh invalid Windows escape characters, preventing immediate run on Linux, have been removed.
-  ARF and OVAL vulnerability XML reports are now UTF-8 encoded to prevent invalid, non-UTF-8 characters from appearing in the report. The presence of these characters, can cause a problem when importing reports into other applications such as CIS-CAT Pro Dashboard.
- The environment command has been enhanced to handle variables configured over multiple lines.
- The ability to disable/enable schema validation now functions when configured in the assessor-cli.properties file.
- The creation of the Linux file item will no longer fail when a file size result is longer than maximum integer size.
- An update was made to the linux file collection process to account for the "xsi:nil=true" value in the filename element.

---------------------------

## CIS-CAT Pro Assessor, v4.0.0 
Release Date: October 26, 2018

This is the initial release of CIS-CAT Pro Assessor v4 (CCPA), a command-line user interface enabling configuration and vulnerability assessment of endpoints.

### Assessor Updates 
- Assessment of the system from which the Assessor is invoked.  This functionality mimics the host-based assessments from CIS-CAT v3.
- Assessment of remote Windows endpoints using WinRM and an "ephemeral" agent.
- Assessment of remote Unix/Linux endpoints using an SSH-based connection.
- Assessment of Cisco IOS network devices using an SSH-based connection.
- Support for the assessment of Security Content Automation Protocol (SCAP) 1.2 data-stream collections.
- Support for the assessment of XCCDF 1.2-based content.
- Support for the assessment of OVAL Definitions files, such as inventory and vulnerability definitions.
- Support for multiple report formats, such as the Asset Reporting Format and OVAL Results with System Characteristics in XML format, as well as HTML, CSV, or plain-text formats.
- Support for the upload of assessment results to CIS-CAT Pro Dashboard.