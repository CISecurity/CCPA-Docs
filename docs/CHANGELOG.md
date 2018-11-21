Change Log
==========

![](http://i.imgur.com/5yZfZi5.jpg)


CIS-CAT Pro Assessor v4
---------------------------
See the CIS-CAT Pro Assessor Coverage Guide for information about supported benchmarks, OVAL schemas/test types, and scripting capabilities.

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