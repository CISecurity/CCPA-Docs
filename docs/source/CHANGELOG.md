![](http://i.imgur.com/5yZfZi5.jpg)

# Change Log #

**NOTE: CIS-CAT Pro Assessor v4 is currently in BETA and this documentation will change as a result of ongoing testing and feedback.  Until the official release of CIS-CAT Pro Assessor v4, please consider this document fluid.**


----------

## CIS-CAT Pro Assessor v4.0.0 ##
See the CIS-CAT Pro Assessor Coverage Guide for information about supported benchmarks, OVAL schemas/test types, and scripting capabilities.

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