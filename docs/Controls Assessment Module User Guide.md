CIS Controls™ Assessment Module User Guide
==========================================

![](http://i.imgur.com/5yZfZi5.jpg)

Introduction
------------
The CIS Controls Assessment Module is designed to help organizations measure their implementation of the CIS Controls.  The Controls Assessment Module functions as a module within CIS-CAT Assessor v4 and can be run much like other assessments, making it compatible with existing CIS-CAT functionality including remote assessments and the CIS-CAT Pro Dashboard.  If you are not familiar with CIS-CAT Assessor v4 and running assessments, please review the Assessor v4 documentation at [https://ccpa-docs.readthedocs.io/en/latest/](https://ccpa-docs.readthedocs.io/en/latest/).

Version 1.0.2 of the Controls Assessment Module focuses on Implementation Group 1 in Windows 10 environments, providing a combination of automated checks and survey questions to cover the 43 Implementation Group 1 CIS Sub-Controls.  For the more procedural Sub-Controls, the Controls Assessment Module allows users to save yes/no answers documenting their implementation of those Sub-Controls.  For Sub-Controls that are conducive to automation, specific settings in the environment are checked to generate a machine-specific pass or fail for that Sub-Control.

For more information about the CIS Controls Implementation Groups, see V7.1 of the CIS Controls at [https://www.cisecurity.org/blog/v7-1-introduces-implementation-groups-cis-controls/](https://www.cisecurity.org/blog/v7-1-introduces-implementation-groups-cis-controls/).

Terms of Use
------------
Use of CIS-CAT Pro Assessor v4 and the Controls Assessment Module is subject to CIS’s Membership Terms of Use and the Terms of Service and Privacy Policy currently in use for our CIS WorkBench site.

Deployment
----------
In order to setup the Controls Assessment Module, download the CIS-CAT Assessor zip file (v4.0.6 or later) that contains the Controls Assessment Module from WorkBench (https://workbench.cisecurity.org/) and follow the standard Assessor v4 setup instructions at [https://ccpa-docs.readthedocs.io/en/latest/User's%20Guide/#deployment](https://www.cisecurity.org/blog/v7-1-introduces-implementation-groups-cis-controls/).

Assessable Operating Systems
----------------------------
The Controls Assessment Module is designed to assess Microsoft Windows 10 machines.  It has not been tested with other operating systems at this point.  Attempting to use the Controls Assessment Module to assess non-Windows 10 machines could result in unpredictable behavior or unreliable results.

Types of Checks in the Controls Assessment Module
-------------------------------------------------
The Controls Assessment Module uses both automated checks and survey questions to assess implementation of the CIS Controls.  The automated checks use PowerShell scripts to measure the machine-specific implementation of a Sub-Control.  The survey question checks utilize user-provided answers to determine if a Sub-Control is successfully implemented.  By default, answers to these survey questions are saved in the Assessor properties file, and can be updated between assessments as the organization’s implementation of these Sub-Controls changes.  These saved answers are used as organization-wide answers that apply to all machines in an assessment.  All checks in the Controls Assessment Module regardless of format, automated or survey question, will come down to a Pass or Fail.

Optionally, survey questions can be configured to be asked interactively during an assessment.  While this allows for more granular machine-specific answers to the questions, it also requires each survey question designated as interactive to be answered at the start of each machine’s assessment.  Providing answers interactively can become tedious for assessments with large numbers of machines or for frequent assessments, so it is recommended that the interactive survey question feature only be used if there are answers to specific survey questions that vary from machine to machine in the organization.

Configuration
-------------
The standard Assessor v4 configuration and session setup options are described at [https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/](https://ccpa-docs.readthedocs.io/en/latest/Configuration%20Guide/).  The information provided there describes various Assessor configuration options including how to setup remote assessments.  In addition to the standard Assessor v4 configuration options, the following Controls Assessment Module specific configuration options are available as well.

### Configurable Values for Automated Checks ###
Additionally, there are four values that can be configured for the automated checks.  If your organization wishes to use different values than the defaults, these values can be updated in the Assessor properties file (config\assessor-cli.properties).  Midway through this file is a section entitled “CAM IG1 Customizable Values”.

![](https://i.imgur.com/5SIzr4Z.png)

<p style="text-align: center;">Customizable Values and Variable Names</p>

These values can be set as appropriate for the organization.  For example, if the organization only requires a password length of 10, the following change could be made:

    xccdf_org.cisecurity_value_4.2_var=10

### Survey Questions ###
Answers to the survey questions can be provided in the Assessor properties file (config\assessor-cli.properties).  The second half of this file has a section entitled “CAM IG1 Survey Questions” containing instructions, question lines, and answer lines.  All of these survey questions are set to a value of “n” by default, meaning that each of these Sub-Controls will be assessed as a “Fail” unless the user changes this value.  For those Sub-Controls that your organization is successfully implementing, the corresponding value should be updated to “y”, meaning that Sub-Control will be assessed as a “Pass”.
For example, by default, the survey question for Sub-Control 12.1 is set as follows:

    ##Sub-Control 12.1 Question: Does your organization maintain an up-to-date inventory of all of the organization’s network boundaries?
	xccdf_org.cisecurity_value_12.1_var=no

If your organization is implementing this Sub-Control, you could change it as follows and save the file:

	##Sub-Control 12.1 Question: Does your organization maintain an up-to-date inventory of all of the organization’s network boundaries?
	xccdf_org.cisecurity_value_12.1_var=yes

For survey questions that you want to provide interactive, machine-specific answers to instead of saving organization-level answers in this properties file, the answer line for that question can be commented out by prepending a “#” at the beginning of the answer line.  This will result in the answer value on that line being ignored, and the question will instead be asked on the Assessor command line for each machine in the assessment:

	##Sub-Control 12.1 Question: Does your organization maintain an up-to-date inventory of all of the organization’s network boundaries?
	#xccdf_org.cisecurity_value_12.1_var=no

Any subset of Sub-Control questions can be selected to be interactive.  None are interactive by default.

Running the Controls Assessment Module
--------------------------------------
Once you have configured the Assessor properties and sessions files appropriately, as well as any Controls Assessment Module specific settings as described above, then you are ready to run the Controls Assessment Module.  There are 3 Controls Assessment Module profiles to choose from:

1.	Implementation Group 1 for Windows 10 (Partial) - Automated Sub-Controls Only
    * This profile runs only the automated checks which currently covers 13 Sub-Controls.
    * Sub-Controls: 3.4, 4.2, 6.2, 8.2, 8.5, 9.4, 10.1, 10.2, 10.4, 13.6, 15.7, 16.9, and 16.11.
2.	Implementation Group 1 for Windows 10 (Partial) - Survey Question Sub-Controls Only
    * This profile runs only the survey questions which currently covers 33 Sub-Controls.
    * Sub-Controls: 1.4, 1.6, 2.1, 2.2, 2.6, 3.5, 4.3, 5.1, 7.1, 7.7, 8.4, 10.5, 11.4, 12.1, 12.4, 13.1, 13.2, 14.6, 15.10, 16.8, 17.3, 17.5, 17.6, 17.7, 17.8, 17.9, 19.1, 19.3, 19.5, and 19.6. 
3.	Implementation Group 1 for Windows 10 (Full) - Automated Checks and Survey Questions
    * This profile runs both the automated checks and the survey questions which covers all 43 of the IG1 Sub-Controls.

The Controls Assessment Module can be run via the CIS-CAT Assessor v4 command line in either of 3 ways (first navigate to the directory where Assessor is installed using a command prompt):

1.	Assessor’s interactive mode (“-i” option)
    * In the command prompt, enter “Assessor-CLI.bat –i”
    * Select the number for “CIS Controls Assessment Module - Implementation Group 1 for Windows 10”
    * When prompted, enter 1, 2, or 3 to select the desired profile
2.	Select the Controls Assessment Module and a profile directly with Assessor’s “-b” option.  In the command prompt, enter one of the following depending on which profile you wish to run:
    * Assessor-CLI.bat -b benchmarks\CIS_Controls_Assessment_Module_v1.0.2-xccdf.xml -p "Implementation Group 1 for Windows 10 (Full) - Automated Checks and Survey Questions"
    * Assessor-CLI.bat -b benchmarks\CIS_Controls_Assessment_Module_v1.0.2-xccdf.xml -p "Implementation Group 1 for Windows 10 (Partial) - Survey Question Sub-Controls Only"
    * Assessor-CLI.bat -b benchmarks\CIS_Controls_Assessment_Module_v1.0.2-xccdf.xml -p "Implementation Group 1 for Windows 10 (Partial) - Automated Sub-Controls Only"
3.	Assessor’s Configuration File XML mode (“-cfg” option)
	
Controls Assessment Module Output
---------------------------------
### Overall Results ###
The results from Controls Assessment Module assessments can be viewed in the same ways that the results from other Assessor assessments can be.  If you have an instantiation of CIS-CAT Pro Dashboard, results can be uploaded there for easy viewing.  This allows you to see score changes over time via Benchmark View.  The Controls View also lets you drill down by Control and see results organized by Sub-Control.
Whether viewing the results in Dashboard or certain other output formats such as HTML, additional information including the Sub-Control number, title, description, rationale, and remediation is available.

### Automated Check Detailed Results ###
You may want to view script-specific outputs for individual Controls Assessment Module automated checks in order to see why a particular check passed or failed.  This information can be viewed in several ways:

1.	HTML file
    * One way to view the outputs of individual automated checks is through an HTML output file.  This file can be generated by appending “-html” to the Assessor command line used to run the Controls Assessment Module.  This will result in an HTML output file being generated for each machine in the assessment.  
    * After opening this file in a browser, it is possible to expand the “Show Rule Result XML” for a particular Sub-Control with an automated check to see additional information.
    * In the expanded text box, look between the <out> and </out> tags to see the output from the PowerShell script.
2.	Assessor Log file	
    * Be sure you run Assessor with at least verbosity level “-vvv” by appending either “-vvv”, “-vvvv” “-vvvvv”, or “-vvvvvv” to the command.
    * In the “logs” folder in the Assessor directory, you can open an appropriate log file that includes the information from a Controls Assessment Module assessment.
    * You can do a Find for “CAM Sub-Control” followed by the number of the Sub-Control that you are interested in.  For example, search for “CAM Sub-Control 4.2”.  This should be followed by the script’s output.

PowerShell
----------
The automated checks in the Controls Assessment Module utilize PowerShell scripts.  These scripts are only designed to read configuration data from target systems.  Efforts have been made so you should not need to change your PowerShell settings in order to run these scripts.  Assessor v4 calls PowerShell using the “-ExecutionPolicy bypass” option.  This will temporarily bypass the existing PowerShell execution policy just for the duration of each Controls Assessment Module script’s run without changing the system’s overall PowerShell execution policy.  Additionally, the Unblock-File PowerShell command will be run against the scripts when CIS-CAT Assessor calls them; this will result in the Controls Assessment Module scripts remaining unblocked/trusted even after running the Controls Assessment Module.  The use of the “-ExecutionPolicy bypass” and “Unblock-File” are meant to contribute to a smoother user experience, but it is important that you consider any policy and security implications for your organization prior to running the Controls Assessment Module.  Currently, the PowerShell scripts for the Controls Assessment Module are not signed.

For more information on PowerShell Execution Policies, see: [https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-6](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-6) to ensure that you understand the security implications of these settings.

Automated Check Design
----------------------
For the automated checks, it was necessary to make decisions about what constituted passing a Sub-Control.  Attempts were made to take into account both Group Policy (GP) and non-GP settings whenever possible.  Similarly, attempts were made to take into account machine-level and user-level settings whenever possible.

### Group Policy ###
Group Policy settings can be either dictated by a domain controller such as Active Directory if the machine is domain-joined, or can be local GP as specified in the Local Group Policy Editor.  Domain settings generally override local machine settings, while local GP settings typically override per-user settings on the machine.  While many of the domain level GP settings overlap with local GP settings, the steps to configure these settings can vary between the two types.  When GP instructions are provided in the Controls Assessment Module, these refer to the Local GP Editor.
GP-enforced settings are generally preferred from a security perspective since they require greater levels of privilege to change, making it harder for a user or attacker to undermine secure settings.  However, when possible, both GP and non-GP settings were factored in to the Controls Assessment Module automated checks to allow for organizations who are not using GP.

### Machine vs. User Settings ###
Similarly, some settings on a machine can apply to the entire machine, or might only apply to particular users on that machine.  (Sometimes, but not always, the distinction for settings stored in the registry is the difference between the HKEY Local Machine and the HKEY Current User registry hives).  From a security perspective, machine settings are preferred to user settings, since they would apply a security policy to the entire machine.  When possible, both types of settings were factored in for the Controls Assessment Module’s automated checks.  It is important to keep in mind, however, that the per-user settings that Controls Assessment Module checks would be those of the user running Assessor or those specified in the Assessor sessions file.
