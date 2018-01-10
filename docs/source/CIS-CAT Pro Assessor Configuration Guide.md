![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor Configuration Guide #

## Introduction ##
Utilizing the CIS-CAT Pro Assessor CLI, users are capable of performing both host-based (local) assessments, as well as remote-based assessments.  In order to perform assessments of remote endpoints, certain configurations must be made.  The intent of this document is to serve as a guide for enabling systems for remote-based assessments using CIS-CAT Pro Assessor.


### Extra configuration Options ###

	-sessions, --sessions <SESSIONS.PROPERTIES>
The `-sessions` option allows users to configure multiple endpoints for assessment of a benchmark.  The `sessions.properties` file configures CIS-CAT Pro Assessor for the assessment of remote endpoints by specifying remote hosts, ports, and credentials which the application will use for connection, collection and evaluation of benchmark recommendations and/or vulnerabilities.  See "Remote Assessment Capability" below for more information.

If no `sessions.properties` file exists or no connections are configured in the file, CIS-CAT Pro Assessor CLI will assess the local machine.