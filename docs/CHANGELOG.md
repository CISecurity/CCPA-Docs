Change Log
==========

![](http://i.imgur.com/5yZfZi5.jpg)


CIS-CAT Pro Assessor v4
---------------------------
See the CIS-CAT Pro Assessor Coverage Guide for information about supported benchmarks, OVAL schemas/test types, and scripting capabilities.

## CIS-CAT Pro Assessor, v4.0.0 ##
#### Release Date: October 26, 2018 ####
This is the initial release of CIS-CAT Pro Assessor v4 (CCPA), a command-line user interface enabling configuration and vulnerability assessment of endpoints.

### Bundle Hashes ###
|Hash Function| Hash                                                            |
|-------------|-----------------------------------------------------------------|
| md5         |88e7064a088771dbd460748bb1de726e                                 |
| sha1        |4ca98117797715961351a4793675917a4195240b                         |
| sha256      |53000be6c94312ef1d3814c4a4d1f87e3f0ae63c4cf28596321f52c1d9ab2014 |

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