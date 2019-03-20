CIS-CAT Pro Assessor CLI User's Guide
=====================================

![](http://i.imgur.com/5yZfZi5.jpg)


Introduction
------------
The CIS-CAT Pro Assessor CLI is a command-line user interface, allowing users to assess target systems against various forms of machine-readable content.  CIS-CAT Pro Assessor CLI is designed primarily to assess CIS Benchmark configuration recommendations but can also assess content written in conformance with the Security Content Automation Protocol (SCAP), as well as plain OVAL definition content.

## Remote Assessment Capability ##
Arguably the most important feature to be included in CIS-CAT Pro Assessor v4 is the ability to assess remote endpoints.  Providing appropriate connection information allows CIS-CAT Pro Assessor to establish a "session", execute commands, run scripts, and perform collection and evaluation for the remote endpoint.  For Microsoft Windows endpoints, this "session" is established through the use of WinRM.  For Unix/Linux and Cisco network device endpoints, CIS-CAT Pro Assessor establishes the "session" via SSH.

Endpoints to be assessed must be configured appropriately to allow for remote access.  Please see the [CIS-CAT Pro Assessor Configuration Guide](./Configuration%20Guide) for more information.

## Cisco Configuration Assessment ##
CIS-CAT Pro Assessor v4 includes the capability to assess Cisco networking devices in two ways.  Users can choose to connect directly to an online network device, via SSH, using a privileged account and perform evaluations against the current running configuration.  New to v4, users now have the ability to export device configurations, specifically the full output of the `show tech-support` command, to a file, and CIS-CAT Pro Assessor v4 can parse that output and perform the assessment.  Specifying the path to the exported configuration file is through the "session" configurations.  Detailed information on "sessions" can be found in the [CIS-CAT Pro Assessor Configuration Guide](./Configuration%20Guide).

## Deployment ##
CIS-CAT Pro Assessor CLI is a simple Java-based application and as such, requires a Java Runtime Environment (JRE) at or above version 1.8, in order to execute.  OpenJDK versions of Java are also supported.  See [https://openjdk.java.net/](https://openjdk.java.net/) for information about these free and open-source implementations of Java.  A suitable JRE/JDK may be installed to the machine on which CIS-CAT is installed, or may be located on a network share.  As long as the machine executing the CIS-CAT Pro Assessor CLI application can access a suitable JRE, it may be used to run the tool.

### A note on benchmark coverage ###
Many benchmarks which utilized CIS' proprietary Embedded Check Language (ECL) ***are not yet supported*** in CIS-CAT Pro Assessor v4, with the exception of the latest Apple OSX versions.  Further development will either implement these benchmarks using currently available scripting capabilities, or will be migrated to OVAL when platform coverage is expanded.  See the [CIS-CAT Pro Assessor Coverage Guide](./Coverage%20Guide) for the most up-to-date information regarding platform coverage.

## Using CIS-CAT Pro Assessor CLI ##
Bundled with the application are two script files; a Microsoft Windows batch script, `Assessor-CLI.bat` and a Unix/Linux shell script, `Assessor-CLI.sh`.  These scripts serve as the entry point to the application.  Any examples included in this user's guide will utilize the Microsoft Windows batch script, but usage of the Unix/Linux shell script can be substituted.

**NOTE: These CIS-CAT scripts must be executed from the command line using root, Administrator, or an equivalently privileged principal.**

## Command Line Options ##
CIS-CAT Pro Assessor CLI can perform a variety of functions related to both benchmark and vulnerability assessments.  The myriad command-line options allow for combined usage to initiate these functions.

### Basic Options ###

Basic operation of CIS-CAT Pro Assessor CLI allows a user to get help, list available content, or to interactively step through the selection of a benchmark and profile prior to executing an assessment.

| Short Option  | Long Option   |  Argument(s)      | Description                    |
| ------------- | ------------- | ------------|---------------------------------- |
| `-h`          | `--help`      | N/A | Display CIS-CAT Pro Assessor help output. |
| `-l`          | `--list`      | N/A | List the benchmarks available for assessment.|
| `-lv`          | `--list-verbose` | N/A |Enable more verbose output when combined with the `-l` option, specifically displaying the full filepath to the benchmark, for later assessment using the `-b` option.|
| `-i`          | `--interactive` | N/A | Execute the Assessor in "interactive" mode specifically for benchmark assessments, allowing the user to manually select a benchmark and profile for assessment.  Based on the selected benchmark, the user may be required to enter "interactive values" which are then used by the assessment engine. |
| `-o`          | `--definitions` | N/A | Execute the Assessor in "interactive" mode specifically for the manual selection and evaluation of OVAL Definitions files, and (optionally) selecting and associating an OVAL Variables file as well.|
| `-d`          | `--startingDir` | `<DIRECTORY>` | Configure the relative root folder from which other options, such as benchmarks, can be found. |
| `-cfg` |`--config-xml`|`<CONFIGURATION XML FILE>`| Execute CIS-CAT Pro Assessor using configuration information found in the `<CONFIGURATION XML FILE>`.  This file allows users to override user properties, configure interactive values, setup sessions and outline the various assessments to be performed.  See the "Using a Configuration XML File" section below for more information and examples regarding the structure and options for the XML configuration file.  Configuration files can be encrypted in order to help protect sensitive data (see the "File Encryption Options" section for details).|

#### Examples ####

Simply display the CIS-CAT Pro Assessor help information:

	> Assessor-CLI.bat -h

List all available benchmarks:

	> Assessor-CLI.bat -l

List all available benchmarks relative to a specific folder:

	> Assessor-CLI.bat -l -d C:\CIS\My-Benchmarks

List All Available Benchmarks (including path information for use with the `-b` option)

	> Assessor-CLI.bat -l -v

Execute an assessment of a benchmark/data-stream in "interactive" mode:

	> Assessor-CLI.bat -i

Execute an assessment of a benchmark/data-stream in "interactive" mode, selecting a benchmark from a location relative to a specific folder:

	> Assessor-CLI.bat -i -d C:\CIS\My-Benchmarks

Execute an assessment of an OVAL Definitions file in "interactive" mode:

	> Assessor-CLI.bat -i -o

Execute an assessment of an OVAL Definitions file in "interactive" mode, selecting the definitions file from a location relative to a specific folder:

	> Assessor-CLI.bat -i -o -d C:\CIS\My-Benchmarks

Execute an assessment or set of assessments using information found in a saved configuration XML file:

	> Assessor-CLI.bat -cfg C:\CIS\assessment-configuration.xml


### Benchmark/Data-Stream Collection Options ###
The benchmark and data-stream collection options provide users the ability to select specific content for assessment.  The `-b` option gives the user the choice to specify the path to either the XCCDF file (containing the `<Benchmark>` element) or the Data-stream collection file.  Using the `-p` option, users can select a specific configuration profile to assess, using either the profile's ID or the profile's title/name.

| Short Option  |  Long Option  |   Argument   | Description                      |
| ------------- | ------------- | -------------|--------------------------------- |
| `-b`          | `--benchmark` | `<BMK-OR-DSC>` | Specify either the full filepath to the assessment content or a path relative to the starting directory.  The `<BMK-OR-DSC>` argument represents either a Benchmark XCCDF file, or the SCAP 1.2-formatted Data-stream Collection file.|
| `-dm`         | `--data-stream` | `<DATA-STREAM>` | Used only when the `-b` option selects a data-stream-collection document, the `-dm` option specifies, within the collection, the ID of the data-stream to be assessed. |
| `-cl` | `--checklist` | `<CHECKLIST>` | Used only in conjunction with the `-dm` option, the `-cl` option specifies, within the data-stream, the ID of the checklist (benchmark) to be assessed.|
| `-p` | `--profile` | `<PROFILE>` | Specify either a profile name, such as `Level-1`, or the profile ID, such as `xccdf_org.cisecurity.benchmarks_profile_Level_1`.  Note that when using the profile name, if any spaces occur, the entire profile name must be wrapped in double-quotes, such as `"Level 2"`|

#### Examples ####

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, automatically selecting the first profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, selecting a specific profile by name:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -p "Level 1 + BitLocker"

Execute an assessment against the CIS Microsoft Windows 10 benchmarks, using an absolute path to the benchmark file, automatically selecting the first profile:

	> Assessor-CLI.bat -b C:\CIS\MyBenchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using the default first data-stream, default first checklist, and default first profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using a specific data-stream, the default first checklist, and default first profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -dm scap_org.cisecurity_datastream_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using a specific data-stream, a specific checklist, and the default first profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -dm scap_org.cisecurity_datastream_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark -cl xccdf_org.cisecurity.benchmarks_benchmark_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using a specific data-stream, a specific checklist and a specific profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -dm scap_org.cisecurity_datastream_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark -cl xccdf_org.cisecurity.benchmarks_benchmark_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark -p "Level 1 - Member Server"


### OVAL Definitions Assessment Options ###
CIS-CAT Pro Assessor also has the ability to assess OVAL definitions files, such as vulnerability definitions downloaded from the OVAL repository.  Using an OVAL Variables file also allows for the injection of "external" variable values into the assessment of OVAL definitions content.

| Short Option  |  Long Option  |   Argument   | Description                      |
| ------------- | ------------- | -------------|--------------------------------- |
| `-od     ` | `--oval-definitions` | `<OVAL_DEFINITIONS>` | Specify either the full filepath to an OVAL Definitions XML file, or a path relative to the starting directory.|
| `-ov` | `--oval-variables` | `<OVAL_VARIABLES>` | Only used in conjunction with the `-od` option, the `-ov` option specifies either the full filepath to an OVAL Variables XML file, or a path relative to the starting directory.|

#### Examples ####

Execute an assessment against the Microsoft Windows 10 vulnerability definitions:

	> Assessor-CLI.bat -od vulnerabilities\microsoft_windows_10.xml

Execute an assessment against the Microsoft Windows 10 vulnerability definitions, producing both an OVAL Result XML file, and an HTML report:

	> Assessor-CLI.bat -od vulnerabilities\microsoft_windows_10.xml -html

Execute an assessment against an OVAL Definitions file containing "external" variables, using an OVAL Variables file to provide those variable values:

	> Assessor-CLI.bat -od C:\CIS\oval_definitions.xml -ov C:\CIS\oval_variables.xml

Execute an assessment against an OVAL Definitions file containing "external" variables, using an OVAL Variables file to provide those variable values, producing both an OVAL Results XML file, and an HTML report:

	> Assessor-CLI.bat -od C:\CIS\oval_definitions.xml -ov C:\CIS\oval_variables.xml -html


### Reporting Options ###
A number of options exist for generating assessment results.  When a benchmark or data-stream collection is assessed, the Asset Reporting Format (ARF) results are generated.  The ARF report is an XML document containing Asset Information for the endpoint under assessment, the benchmark/data-stream that was assessed, system characteristics, and assessment results.  When OVAL Definitions are assessed, an "OVAL results with system characteristics" XML document is produced by default.  These reports are automatically generated and cannot be disabled.  These XML documents are designed to be either uploaded directly to CIS-CAT Pro Dashboard, or transformed into more human-readable HTML, CSV or plain-text documents.

The following table summarizes a number of options controlling which reports to generate, naming of reports, and functionality allowing users to upload reports to a URL, such as CIS-CAT Pro Dashboard.

| Short Option  |   Long Option   |    Argument   | Description                       |
| ------------- | --------------- | --------------|---------------------------------- |
| `-rd`         | `--reports-dir` | `<DIRECTORY>` | Configure the report destination folder, allowing users to configure the location to which result reports are written.|
| `-rp`         | `--report-prefix` | `<PREFIX>` | Configure the "front" portion of the report name generated by the tool.  Every report will automatically be of the format `[report-prefix]-[timestamp].[extension]` such as `CIS-CAT-TEST-Windows10-20171218T173220Z.xml`.|
| `-html` | N/A | N/A | Generate an HTML report.  The report name will be of the format `[report-prefix]-[timestamp].html`|
| `-csv` | N/A | N/A | Generate a CSV report.  The report name will be of the format `[report-prefix]-[timestamp].csv`|
| `-txt` | N/A | N/A | Generate a plain text report.  The report name will be of the format `[report-prefix]-[timestamp].txt`|
| `-u` | `--url`| `<REPORTS-URL>` | Specify a URL to which Assessor results are uploaded, using HTTP(S) POST.|
| `-ui` | `--ignore-warnings` | N/A | Indicate that, when uploading results to a URL via the `-u` option, any SSL certificate warnings should be ignored.|
| `-narf` | `--no-arf` | N/A| This option disables the generation of Asset Reporting Format (ARF) XML results.  The ARF report is the default report generated by the Assessor.|
| `-nrf` | `--no-report-file` | N/A | This option disables generation of a results report file.  When utilizing the `-u` option, Assessor results are uploaded to the supplied URL.  In that use-case, report files are generally not needed.|

#### Examples ####
Execute CIS-CAT Pro Assessor CLI interactively, generating both an Asset Reporting Format result (by default) and an HTML report, saving them to the default reports folder:

	> Assessor-CLI.bat -i -html

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, automatically selecting the first profile.  Generate both the Asset Reporting Format (ARF) by default and an HTML report.  Save the reports to a specific reports folder:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -html -rd C:\CIS\custom\reports

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, automatically selecting the first profile.  Generate both the Asset Reporting Format (ARF) by default and an HTML report.  Save the reports to the default reports folder, but name the reports in a custom format:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -html -rp "CCPA-Windows10"

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, automatically selecting the first profile.  Configure the application to not generate any physical report files, but to upload the results to CIS-CAT Pro Dashboard, ignoring any SSL certificate warnings:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -nrf -u https://ccpd.example.org/CCPD/api/reports/upload -ui


### Logging Options ###
The following table describes the various options to control the application log file generation.  By default, the Assessor-CLI application is configured to log at the WARN level.

| Short Option  |   Long Option   |    Argument   | Description                       |
| ------------- | --------------- | --------------|---------------------------------- |
| -nl           | --no-logging    | N/A | Disable all logging.
| -v            | --error         | N/A | Only write log messages with a level of ERROR.|
| -vv           | --warn          | N/A | Write log messages with a level of WARN or ERROR.|
| -vvv          | --info          | N/A | Write log messages with a level of WARN, ERROR, or INFO.|
| -vvvv         | --debug         | N/A | Write log messages with a level of WARN, ERROR, INFO, or DEBUG.|
| -vvvvv        | --trace         | N/A | Write log messages with a level of WARN, ERROR, INFO, DEBUG, or TRACE.|
| -vvvvvv       | --all           | N/A | Write all log messages.|

#### Examples ####
Execute an "interactive" assessment at the INFO log level:

	> Assessor-CLI.bat -i -vvv

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the Level 2 profile, writing log messages at the DEBUG log level:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -p "Level 2" -vvvv


### Miscellaneous Options ###

| Short Option  |   Long Option   |    Argument   | Description                       |
| ------------- | --------------- | --------------|---------------------------------- |
| `-vdd` | `--vulnerability-definitions` | N/A | Download the latest supported vulnerability definitions.  See the [CIS-CAT Pro Assessor Coverage Guide](./Coverage%20Guide) for the most up-to-date information regarding vulnerability definitions platform coverage.  Vulnerability definitions files are saved into the application's `vulnerabilities` folder, i.e. `C:\CIS\Assessor-CLI\vulnerabilities`.|
| `-sessions`| `--sessions`| `<SESSIONS.PROPERTIES>`| The `-sessions` option allows users to configure multiple endpoints for assessment of a benchmark.  The `sessions.properties` file configures CIS-CAT Pro Assessor for the assessment of remote endpoints by specifying remote hosts, ports, and credentials which the application will use for connection, collection and evaluation of benchmark recommendations and/or vulnerabilities.  See "Remote Assessment Capability" below for more information.  <br/><br/>If no `sessions.properties` file exists or no connections are configured in the file, CIS-CAT Pro Assessor CLI will assess the local machine.  Sessions.properties files can be encrypted in order to help protect sensitive data (see the "File Encryption Options" section for details).|
| `-props`| `--properties`| `<PROPERTIES-FILE>`| The CIS-CAT Pro Assessor CLI user properties file defaults many runtime properties used during the assessment process.  These properties may be customized per assessment or per endpoint, by creating individual properties files, and specifying either the full filepath or a path relative to the working directory.  If this option is not specified, CIS-CAT Pro Assessor CLI will load a default properties file named `assessor-cli.properties` located in the `config` folder of the application installation.|
| `-D`| N/A| `<Property=Value>`| Instead of creating a new properties file for unique assessments, individual user properties may be specified using the `-D` option together with a `property=value` pair.  This allows an assessment to only override specific user properties when only a small number differ from the defaults.|
| `-test` | `--test`| N/A | The `-test` option allows the user to perform connection tests on any sessions configured to execute during the assessments.  These sessions may be loaded from a configuration XML file (`-cfg`) or from a sessions.properties file (`-sessions`).  When specified, connectivity tests are performed and reported to the user on the CIS-CAT Pro Assessor console.  Once completed, CIS-CAT Pro Assessor exits.  When the `-test` option is supplied, no assessments take place; only the connectivity tests.|
| `-q`| `--quiet`| N/A | Enable the Assessor to execute in "quiet mode", causing the suppression of any assessment status information from being written to the console.|

#### Examples ####
Download the latest vulnerability definitions:

	> Assessor-CLI.bat -vdd

Download the latest vulnerability definitions when using an HTTPS Proxy:

	> Assessor-CLI.bat -vdd -D https.proxyHost=PROXY_HOSTNAME_OR_IP -D https.proxyPort=PROXY_PORT

Download the latest vulnerability definitions when using an HTTP Proxy:

	> Assessor-CLI.bat -vdd -D http.proxyHost=PROXY_HOSTNAME_OR_IP -D http.proxyPort=PROXY_PORT

Execute a vulnerability assessment for the Microsoft Windows Server 2012 R2 platform, producing both an OVAL Result XML file, and an HTML report:

	> Assessor-CLI.bat -od vulnerabilities\microsoft_windows_server_2012_r2.xml -html

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, automatically selecting the first profile, assessing a number of remote machines, configured in a specific session configuration file:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -sessions C:\CIS\sessions\windows_10_machines.properties


Execute an assessment against the CIS Oracle Database 11g R2 benchmark, selecting the Windows Server Host OS profile, and configuring the required "interactive" values:

	> Assessor-CLI.bat -b benchmarks\CIS_Oracle_Database_11g_R2_Benchmark_v2.2.0-xccdf.xml -p "Level 1 - Windows Server Host OS" -D xccdf_org.cisecurity_value_jdbc.url=jdbc:oracle:thin:user/s3cr3t@DBHOST:1521:devdb -D xccdf_org.cisecurity_value_listener.ora=C:\product\oracle\network\admin\listener.ora

Using a customized properties file defining session connections, test the connectivity of each session and exit:

	> Assessor-CLI.bat -sessions config\test-sessions.properties -test

Execute the Assessor, against the CIS Microsoft Windows 10 benchmark, in "quiet mode"

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -q


### File Encryption Options ###
To help protect sensitive data, such as target system login credentials, configuration XML files and sessions.properties files used to drive the assessment process can be encrypted via use of a password.  An encrypted copy of the source file is created and written to the `config` folder, preserving the plaintext source file for possible future updates and as a backup in case the password used to encrypt the file is forgotten or lost.  The name of the encrypted file will be **"enc_"** followed by the source file's name.  The plaintext source files should be stored in a secure location after creating an encrypted copy of them.  The same password used to encrypt a particular file is also used by the Assessor to decrypt that file in memory for use in the assessment process.

Encryption passwords can include special characters.  Many special characters do not need to be escaped when they are used within a quoted string, but certain characters may cause unanticipated consequences.  For example, the percent (%) character has a special meaning for command line parameters in Windows and should be escaped if you intend to use it in a password.  To help ensure passwords are processed appropriately, **it is recommended to enclose passwords in quotes both when encrypting a file and when using an encrypted file in the assessment process.**  The quotes handle most special characters without having to escape those characters and are necessary to preserve any blank spaces in a password.  **Use double quotes on the Windows command line and single quotes for Unix/Linux.**

| Short Option  |   Long Option   |    Argument   | Description                       |
| ------------- | --------------- | --------------|---------------------------------- |
| `-e` | `--encrypt` | `<FILE TO ENCRYPT>` | The full path to the sessions.properties file or configuration.xml file to be encrypted, including the file name and its extension.|
| `-ep`| `--encryption-password`| `<ENCRYPTION PASSWORD>`| The password that will be used to encrypt a sessions.properties file or configuration.xml file.  It is recommended to enclose this password in quotes.|
| `-fp`| `--file-password`| `<FILE PASSWORD>`| The password originally used to encrypt a sessions.properties file or configuration.xml file.  This command line option is used in conjunction with the `-cfg` and `-sessions` options when utilizing an encrypted configuration XML file or sessions.properties file.  It is recommended to enclose this password in quotes.|

#### Examples ####
Encrypt a configuration XML file:

	> Assessor-CLI.bat -e C:\Test\config_file.xml -ep "MyP@ssword$@!*&"

Use an encrypted configuration XML file in the assessment process:

	> Assessor-CLI.bat -cfg C:\Test\enc_config_file.xml -fp "MyP@ssword$@!*&"


#### Configuring Interactive Values ####
A number of benchmarks supported by/bundled with CIS-CAT Pro Assessor require manual interaction by the user in order to configure specific values used during the assessment.  These "interactive values" will be presented to the user during a manual execution of the assessment, but will block the completion of the assessment if it is being executed off-hours, or as part of an automated script.  CIS-CAT Pro Assessor provides a mechanism for these "interactive values" to be configured using a properties file, thus removing the burden of entering these values manually.  This configuration requires knowledge of the value's `id` attribute within the benchmark or data-stream collection component.  The [CIS-CAT Pro Assessor Coverage Guide](./Coverage%20Guide) provides a listing, for each applicable benchmark, for any "interactive value" `id` attributes.  Once known, a user can modify the `assessor-cli.properties` file to specify the value:

	xccdf_org.cisecurity_value_jdbc.url=jdbc:oracle:thin:system/manager@dbhost:1521:orcl

When CIS-CAT Pro Assessor executes, the program will (by default) attempt to load properties contained in the `config\assessor-cli.properties`.

A second method to configure "interactive values" is to utilize the `-D <Property=Value>` command-line option.  This allows the user to configure a single property at a time when executing, therefore eliminating the potential need for multiple properties files.  Configuring this option on the command-line is straightforward, where the property name is the `id` attribute of the "interactive value" and the property value is configured:

	> Assessor-CLI.bat -b benchmarks\CIS_Oracle_Database_11g_R2_Benchmark_v2.2.0-xccdf.xml -p "Level 1 - Windows Server Host OS" -D xccdf_org.cisecurity_value_jdbc.url=jdbc:oracle:thin:user/s3cr3t@DBHOST:1521:devdb

## Using a Configuration XML File ##
CIS-CAT Pro Assessor can be executed using the `-cfg` option, and specifying a configuration XML file.  This XML file allows user to configure sessions, assessments, interactive values, user properties, and reporting options all in a single file.  This configuration XML file essentially allows for multiple benchmark assessments against multiple endpoints both local and/or remote.

An XML schema is included in the CIS-CAT Pro Assessor CLI bundle, along with a sample configuration file.

### Using Special Characters in XML Elements ###
Some user-entered characters in the XML configuration file may need to be replaced with their numeric character reference equivalent to work properly.  For example, an ampersand (&) character to be used in a password for the credentials element should be replaced with the decimal character reference `&#38;`.  See the full list of decimal character references at [https://en.wikipedia.org/wiki/Numeric_character_reference](https://en.wikipedia.org/wiki/Numeric_character_reference "Numeric Character References").

### Configuration XML Elements ###
The root element of the configuration XML file is `<configuration>`, and utilizes a default namespace URI of `http://cisecurity.org/ccpa/config`.  This namespace URI must be specified or else validation of the configuration XML file will fail.  The root of any XML configuration file should appear as follows:

	<configuration xmlns="http://cisecurity.org/ccpa/config">

All other elements must be contained within the `<configuration>` element.

The following sections describe the elements that are available for configuration through the XML file:

#### CIS-CAT Pro Assessor "starting directory" ####
	<starting_dir>C:\Projects\CIS-CAT\Assessor-CLI</starting_dir>
The `starting_dir` element is optional and contains a value noting the base directory from which any relative paths are specified (such as the location of an XCCDF benchmark).  This element is the equivalent of the `-d` command-line option.  If this element is not present in the configuration file, the default starting directory, the folder in which CIS-CAT Pro Assessor is installed, is used.

#### Vulnerability Definitions Download ####
	<vulnerability_definitions download="(true|false)"/>
The `vulnerability_definitions` element contains a single attribute, `download`.  If this attribute's value is `true`, CIS-CAT Pro Assessor will download the latest vulnerability definitions.  This element/attribute is equivalent to the `-vdd` command-line option.  If this element is not present in the configuration file, or the `download` attribute is set to `false`, vulnerability definitions will not be downloaded.

#### Sessions ####
The `sessions` element configures each individual connection to either the local host or a remote endpoint.  An attribute of the `sessions` element, `test` indicates whether this configuration file is meant to test the connectivity of each session only.  When the `test` attribute is `true`, connectivity tests will take place, and CIS-CAT Pro Assessor will then exit.  No other assessment processing will take place.

	<!-- Session configurations referenced by the assessments -->
	<sessions test="(true|false)">
		
		<!-- A "connection" to the local host -->
		<session id="local">
			<type>local</type>
			<tmp_path>C:\Temp</tmp_path>
		</session>
		
		<!-- A connection to a remote Ubuntu instance using a private key file -->
		<session id="aws-ubuntu">
			<type>ssh</type>
			<host>11.22.33.44</host>
			<port>22</port>
			<user>ubuntu</user>
			<identity>C:\Path\To\aws-ubuntu.ppk</identity>
			<tmp_path>/path/to/temp/folder</tmp_path>
		</session>
		
		<!-- A connection to a remote CentOS instance using a private key file secured with a passphrase -->
		<session id="aws-centos">
			<type>ssh</type>
			<host>1.2.3.4</host>
			<port>22</port>
			<user>centos</user>
			<identity>C:\Path\To\aws-centos.ppk</identity>
			<identity_passphrase>P@55phr@s3!</identity_passphrase>
			<tmp_path>/path/to/temp/folder</tmp_path>
		</session>
		
		<!-- A connection to a remote Windows instance using credentials -->
		<session id="aws-2012r2">
			<type>windows</type>
			<host>AWS-WIN2012R2-AMI</host>
			<port>5986</port>
			<user>Administrator</user>
			<credentials>P@ssw0rd12345</credentials>
		</session>
		
		<!-- A connection to a Cisco IOS device, using a private key file -->
		<session id="cisco-ios1">
			<type>ios</type>
			<host>55.66.77.88</host>
			<port>22</port>
			<user>ciscoprivd</user>
			<identity>C:\Path\To\cisco-ios-private-key.ppk</identity>
			<enable_password>3n@bl3mePlz</enable_password>
		</session>
	</sessions>

Each `session` consists of a number of elements configuring the connection to the target endpoint:

- `id`: Each session must have a unique id.
- `type`:  The session `type` indicates a "flavor" of the connection to the endpoint being assessed.  A number of options exist for the `type` value, as noted in the [CIS-CAT Pro Assessor Configuration Guide](./Configuration%20Guide).
	- **`local`**:  The "local" session type indicates that the assessment(s) will be performed in a host-based manner.  No further session information is required when using a "local" session.
	- **`ssh`**:  The "ssh" session type indicates the connection is to a remote Unix/Linux/Mac endpoint.  This session type allows CIS-CAT Pro Assessor to utilize the `host`, `port`, `user`, and either `credentials` and/or `identity` (and optionally an `identity_passphrase`) to create a SSH connection to the endpoint and use that SSH connection to execute the assessment.
	- **`windows`**:  The "windows" session type indicates (obviously) a connection to a remote Microsoft Windows endpoint.  This session type allows CIS-CAT Pro Assessor to utilize the `host`, `port`, `user`, `credentials` to initiate a WinRM connection to the remote endpoint.
	- **`ios`**:  The "ios" session type indicates a connection to a remote Cisco IOS device, such as a router or switch.  This session type allows CIS-CAT Pro Assessor to utilize the `host`, `port`, `user`, and either `credentials` and/or `identity` (and optionally an `identity_passphrase`) to create a SSH connection to the endpoint and use that SSH connection to execute the assessment.
- `host`:  The "host" element value is either the hostname or IP address of the endpoint to which this session will connect/assess.
- `port`:  The "port" element value is the port number on which communication takes place.  For `ssh` or `ios` connections, the default value for `port` is 22.  For `windows` sessions, the default value is 5986.
- `user`:  The "user" element value specifies the username used to log on to the remote endpoint.  For `ssh` sessions, this user should be either `root` or a username with the ability to `sudo`, in order to elevate privileges to execute the required commands.  For `windows` sessions, the user must be either an Administrator or a member of the Administrators group.  For `ios` sessions, the user must be privileged and able to enter into "enable" mode on that device, using the `enable_password` value below.
- `credentials`:  The "credentials" element identifies the user's password for logging on to the remote endpoint.  Note that this XML file will then be storing users and passwords for remote endpoints, and should thus be secured as much as possible on the machine hosting CIS-CAT Pro Assessor.  When the session type is either `ssh` or `ios`, the `credentials` element can be bypassed by logging into the remote endpoint using a private key file, the path of which is configured in the `identity` element.  If a private key is used for authentication, the `credentials` element can either be left out of the `session` configuration, or included for use when commands must be executed with elevated privileges using `sudo`, and the credentials are required for that user.
- `identity`:  The `identity` element specifies the full filepath to a private key file to be used for authenticating the `user` to the remote endpoint.  When configuring a `session`, the `identity` may require the specification of the `identity_passphrase` in order for authentication to complete successfully.  Note that for `windows` sessions, private key authentication is not currently supported.
- `identity_passphrase`: The `identity_passphrase` element contains credentials required to complete authentication using the private key specified in the `identity` element. If this element exists for a session, but its value is left blank in the file, the user will be prompted to enter the passphrase for that session on the command line as part of initializing all of the sessions at the beginning of an assessment.
- `enable_password`:  When authenticating a privileged user for `ios` sessions, the `enable_password` is mandatory.  This element specifies the credentials which allow the privileged user to enter "enable" mode on the Cisco IOS device.
- `tmp_path`: Configure a custom "temp" directory location for use in creating the "ephemeral" directory on the target endpoint.  The "ephemeral" directory is named `ccpa-temp-TIMESTAMP` and is created as a sub-folder of the directory specified in this setting.  For example, if `tmp_path` is specified as `C:\Temp`, the "ephemeral" directory will be created at `C:\Temp\ccpa-temp-TIMESTAMP`.  **NOTE**: When specifying a value for `tmp_path`, this directory MUST ALREADY EXIST on the target endpoint.  In the above example, if the `C:\Temp` folder does not exist, the connection from CIS-CAT Pro Assessor v4 will not succeed.  If this property is left blank or not included, the Assessor will use the default "temp" folder as defined for the operating system, such as `/tmp` or `C:\Windows\Temp`.  Further information regarding the `tmp_path` and considerations for Unix/Linux environments can be found in the [CIS-CAT Pro Assessor Configuration Guide](./Configuration%20Guide).


#### Assessments ####
The `assessments` element configures which assessment content will be evaluated, against which `session` that content will be assessed, any User properties specific to that assessment, and/or any "interactive" values to be applied to that assessment.

	<assessments>
		<!-- XCCDF COLLECTIONS -->
		<benchmark xccdf="benchmarks\CIS_Ubuntu_Linux_16.04_LTS_Benchmark_v1.0.0-xccdf.xml" profile="Level 1 - Workstation" session-ref="aws-ubuntu"/>
		<benchmark xccdf="benchmarks\CIS_Ubuntu_Linux_16.04_LTS_Benchmark_v1.0.0-xccdf.xml" profile="Level 1 - Server" session-ref="aws-ubuntu"/>
		
		<benchmark xccdf="benchmarks\CIS_Microsoft_Windows_Server_2012_R2_Benchmark_v2.2.1-xccdf.xml" profile="Level 1 - Member Server" session-ref="aws-2012r2">
			<properties>
				<property name="ignore.platform.mismatch">true</property>
			</properties>
		</benchmark>
		
		<benchmark xccdf="benchmarks\CIS_Oracle_Database_11g_R2_Benchmark_v2.2.0-xccdf.xml" profile="Level 1" session-ref="aws-ubuntu">
			<interactive_values>
				<value id="xccdf_org.cisecurity_value_jdbc.url">jdbc:oracle:thin:sys/passw0rd1@DB-SERVER:1521:ORCL</value>
				<value id="xccdf_org.cisecurity_value_listener.ora">/opt/oracle/product/oracle11g/network/admin/listener.ora</value>
			</interactive_values>
		</benchmark>
		
		<!-- DATA-STREAM COLLECTIONS -->
		<data-stream-collection collection="dsc-id" data-stream="ds-id" checklist="benchmark-id" profile="profile-id-or-name" session-ref="local"/>
		
		<!-- OVAL DEFINITIONS COLLECTIONS -->
		<oval_definitions definitions="vulnerabilities\microsoft_windows_10.xml" session-ref="local"/>
		<oval_definitions definitions="definitions\defs.xml" variables="definitions\vars.xml" session-ref="local"/>
	</assessments>

A number of elements may be configured, allowing various assessments against a number of different sessions:

**Assess an XCCDF `<Benchmark>`, selecting the first Profile**:

	<benchmark xccdf="benchmarks\CIS_Ubuntu_Linux_16.04_LTS_Benchmark_v1.0.0-xccdf.xml" session-ref="aws-ubuntu"/>
- `xccdf`: The "xccdf" attribute defines the path (relative to the `starting_dir` or absolute) to the XCCDF file being assessed.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.

**Assess an XCCDF `<Benchmark>`, selecting a named Profile**:

	<benchmark xccdf="benchmarks\CIS_Ubuntu_Linux_16.04_LTS_Benchmark_v1.0.0-xccdf.xml" profile="Level 1 Workstation" session-ref="aws-ubuntu"/>
- `xccdf`: The "xccdf" attribute defines the path (relative to the `starting_dir` or absolute) to the XCCDF file being assessed.
- `profile`: The "profile" attribute defines the configuration Profile, within the XCCDF, selected for assessment.  The value of this attribute may be either the Profile `<title>` or `id` specified in the Benchmark XCCDF.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.

**Assess an XCCDF `<Benchmark>`, selecting a named Profile, and configuring specific assessment properties**:

	<benchmark xccdf="benchmarks\CIS_Microsoft_Windows_Server_2012_R2_Benchmark_v2.2.1-xccdf.xml" profile="Level 1 Member Server" session-ref="aws-2012r2">
		<properties>
			<property name="ignore.platform.mismatch">true</property>
		</properties>
	</benchmark>
- `xccdf`: The "xccdf" attribute defines the path (relative to the `starting_dir` or absolute) to the XCCDF file being assessed.
- `profile`: The "profile" attribute defines the configuration Profile, within the XCCDF, selected for assessment.  The value of this attribute may be either the Profile `<title>` or `id` specified in the Benchmark XCCDF.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.
- `properties`: The "properties" element serves as a container for individual `property` elements.  A `properties` element must contain 1..n `property` element(s).
- `property`: A "property" defines a name/value pair, configuring a single user property named by the value of the `name` attribute.  The value of the `property` is the content of the element.  An individual `property` is the equivalent of using the `-D name=value` command-line option, or a property defined in the "assessor-cli.properties" file, located in the `config` folder.

**Assess an XCCDF `<Benchmark>`, selecting a named Profile, configuring specific values normally requested from the user**:

	<benchmark xccdf="benchmarks\CIS_Oracle_Database_11g_R2_Benchmark_v2.2.0-xccdf.xml" profile="Level 1" session-ref="aws-ubuntu">
		<interactive_values>
			<value id="xccdf_org.cisecurity_value_jdbc.url">jdbc:oracle:thin:sys/passw0rd1@DB-SERVER:1521:ORCL</value>
			<value id="xccdf_org.cisecurity_value_listener.ora">/opt/oracle/product/oracle11g/network/admin/listener.ora</value>
		</interactive_values>
	</benchmark>
- `xccdf`: The "xccdf" attribute defines the path (relative to the `starting_dir` or absolute) to the XCCDF file being assessed.
- `profile`: The "profile" attribute defines the configuration Profile, within the XCCDF, selected for assessment.  The value of this attribute may be either the Profile `<title>` or `id` specified in the Benchmark XCCDF.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.
- `interactive_values`: The "interactive_values" element serves as a container for individual `value` elements.  An `interactive_values` element must contain 1..n `value` element(s).
- `value`: A "value" defines an id/value pair, configuring a single interactive value identified by the `id` attribute.  This `id` attribute should match the `id` of a `<Value>` element in the XCCDF that is noted as `interactive="true"`.  The value of the `value` is the content of the element.  An individual `value` is the equivalent of using the `-D name=value` command-line option, or a property defined in the "assessor-cli.properties" file, located in the `config` folder.

**Assess a SCAP `<data-stream-collection>`, selecting the first data-stream, checklist, and profile**:

	<data-stream-collection collection="collections\collection.xml" session-ref="local"/>
- `collection`: The "collection" attribute defines the path (relative to the `starting_dir` or absolute) to the SCAP 1.2 data-stream collection file being assessed.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.

**Assess a SCAP `<data-stream-collection>`, selecting a named data-stream, the first checklist, and first profile**:

	<data-stream-collection collection="collections\collection.xml" data-stream="ds-id" checklist="benchmark-id" profile="profile-id-or-name" session-ref="local"/>
- `collection`: The "collection" attribute defines the path (relative to the `starting_dir` or absolute) to the SCAP 1.2 data-stream collection file being assessed.
- `data-stream`: The "data-stream" attribute specifies the `id` of the `data-stream`, contained in the collection, to be selected for assessment.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.

**Assess a SCAP `<data-stream-collection>`, selecting a named data-stream, a named checklist, and the first profile**:

	<data-stream-collection collection="collections\collection.xml" data-stream="ds-id" checklist="benchmark-id" profile="profile-id-or-name" session-ref="local"/>
- `collection`: The "collection" attribute defines the path (relative to the `starting_dir` or absolute) to the SCAP 1.2 data-stream collection file being assessed.
- `data-stream`: The "data-stream" attribute specifies the `id` of the `data-stream`, contained in the collection, to be selected for assessment.
- `checklist`: The "checklist" attribute specifies the `id` of the checklist to be assessed.  A checklist is a component in the data-stream collection representing an XCCDF `<Benchmark>`.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.

**Assess a SCAP `<data-stream-collection>`, selecting a named data-stream, a named checklist, and a named profile**:

	<data-stream-collection collection="collections\collection.xml" data-stream="ds-id" checklist="benchmark-id" profile="profile-id-or-name" session-ref="local"/>
- `collection`: The "collection" attribute defines the path (relative to the `starting_dir` or absolute) to the SCAP 1.2 data-stream collection file being assessed.
- `data-stream`: The "data-stream" attribute specifies the `id` of the `data-stream`, contained in the collection, to be selected for assessment.
- `checklist`: The "checklist" attribute specifies the `id` of the checklist to be assessed.  A checklist is a component in the data-stream collection representing an XCCDF `<Benchmark>`.
- `profile`: The "profile" attribute defines the configuration Profile, within the checklist, selected for assessment.  The value of this attribute may be either the Profile `<title>` or `id` specified in the Benchmark XCCDF.
- `session-ref`: The "session-ref" attribute specifies the `id` of a `session` configured in the `sessions` configuration, described above.

**Assess an `<oval_definitions>` file that does not include an `<oval_variables>` file**:

	<oval_definitions definitions="vulnerabilities\microsoft_windows_10.xml" session-ref="local"/>
- `definitions`: The "definitions" attribute defines the path (relative to the `starting_dir` or absolute) to the OVAL Definitions file being assessed.

**Assess an `<oval_definitions>` file that includes an `<oval_variables>` file**:

	<oval_definitions definitions="definitions\defs.xml" variables="definitions\vars.xml" session-ref="local"/>
- `definitions`: The "definitions" attribute defines the path (relative to the `starting_dir` or absolute) to the OVAL Definitions file being assessed.
- `variables`: The "variables" attribute defines the path (relative to the `starting_dir` or absolute) to the OVAL Variables file used in the assessment.

#### Report Output Options ####
The `reports` element contains a number of attributes controlling the output report formats, and sub-elements controlling report output directory, POST URL, and report naming.  The `html` attribute value controls the generation of HTML reports, the `csv` attribute controls the generation of CSV reports, and the `txt` attribute controls the generation of plain-text reports.  The `no-arf` attribute, when `true`, disables the generation of the Asset Reporting Format XML results.  The `no-report-file` attribute, when `true`, overrides the other 3 attributes and disables the generation of any report files.  Setting this attribute to `true` is intended to be used in conjunction with the `reports_url` element, which identifies a URL to which report output should be POST'ed.  If the reports are POST'ed to the URL, they may not need to be generated and saved in file format.
	<reports html="(true|false)" csv="(true|false)" txt="(true|false)" no-arf="(true|false)" no-report-file="(true|false)">
        
        <!-- Customize the folder to which CIS-CAT reports are saved.  If not present, CIS-CAT will use the default reports location. -->
        <reports_dir>C:\Projects\CIS\reports</reports_dir>
        
        <!-- POST the Asset Reporting Format or OVAL Results XML to a URL, ignoring SSL certificate warnings if specified -->
        <reports_url ignore_certificate_warnings="true">https://example.cisecurity.org/CCPD/api/reports/upload</reports_url>
        
        <!-- Override the default report name.  Timestamp information will always be appended to the report_prefix -->
        <reports_prefix>CIS-CAT-DEV</reports_prefix>
    </reports>

Various sub-elements are available to configure the destination folder for report files to be saved, URL's to which reports can be uploaded, and naming of reports:

	<reports_dir>C:\Projects\CIS\reports</reports_dir>
The `reports_dir` element is optional and contains a value noting the directory to which reports are saved.  This element is equivalent to the `-rd` command-line option.

	<reports_url ignore_certificate_warnings="(true|false")>
The `reports_url` element is optional and contains a value noting the URL to which reports are POST'ed.  This element is the equivalent to the `-u` command-line option.  The optional `ignore_certificate_warnings` attribute, when `true`, indicates to CIS-CAT that any SSL certificate warnings should be ignored.  This attribute is the equivalent to the `-ui` command-line option.

	<reports_prefix>CIS-CAT-DEV</reports_prefix>
The `reports_prefix` element is optional and contains a value defining a prefix, essentially naming the reports that are generated by the assessments.  When reports are generated, the name of the report is created by concatenating the reports prefix, the report type (such as ARF or OVALResults) and the timestamp of report generation.  If this element is not present, the default reports prefix is the assessment target's hostname plus the benchmark's title, such as `CIS-CAT-DEV-CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark`.


## Assessing Multiple Windows Targets ##
It is possible to assess a population of Microsoft Windows targets in an automated manner without installing CIS-CAT or the JRE on each target. The following diagram depicts this deployment pattern:

![](https://i.imgur.com/gGUgx7K.png)

### CIS Host Server ###
The *CIS Host Server* is where the CIS-CAT bundle, Java Runtime Environment, and Reports are placed. Targets within the Workstations Group will access these resources to perform a self-assessment using CIS-CAT.

### Workstations Group ###
The *Workstations Group* represents a population of Microsoft Windows targets to be assessed with CIS-CAT. The Domain Administrator will create Group Policy that causes devices in this group to invoke CIS-CAT via a Scheduled Task.  In order to maintain a secure configuration of the CIS Host Server, authenticated users should only be allowed to execute the “cis-cat-centralized.bat” and "cis-cat-centralized-ccpd.bat" files.

### Prerequisites ###
1. All targets must be joined to an Active Directory Domain
2. All targets must have read access to the *CIS-CAT Share* hosted off of the *CIS Host Server*

### Setup ###
Perform the following steps to cause the *Workstations Group* to execute the CIS-CAT instance on the *CIS Host Server*.

#### Create CIS Share on the CIS Hosting Server ####
1. Create a shared folder on the *CIS Host Server* named **CIS**. Share permissions on the CIS folder should allow the Authenticated Users group the ability to both **Read** and **Change** information in the folder. To configure the permissions on the CIS share, right-click on the CIS folder and select “Properties”. Click on the “Sharing” tab, and select “Advanced Sharing”:

![](https://i.imgur.com/XvCEvEJ.png)

From the “Advanced Sharing” popup, select “Permissions”:

![](https://i.imgur.com/Md8TqnE.png)

On the “Permissions” popup, grant **Change** and **Read** to the Authenticated Users group:

![](https://i.imgur.com/KiAmbP0.png)

2. Unzip the CIS-CAT bundle within the **CIS** folder on the *CIS Host Server* and move the Assessor-CLI folder to the root of the **CIS** folder.
3. Create the following directories beneath the CIS folder on the *CIS Host Server*:
	- Java
	- Java64
	- Reports 
4. To copy the java runtime (JRE) to the CIS folder do the following:
	- Browse to the location where Java is installed, by default Java is located at “%ProgramFiles%\Java”.
	- Copy the 32-bit JRE that applies to the targets you will be evaluating, such as jre1.8.0_201, to the Java folder you created in step 3.
	- Copy the 64-bit JRE that applies to the targets you will be evaluating, such as jre1.8.0_201, to the Java64 folder you created in step 3.
5. Move the Assessor-CLI\misc\Windows\cis-cat-centralized.bat file or the Assessor-CLI\misc\Windows\cis-cat-centralized-ccpd.bat file to the root of the CIS folder, depending on whether you want to write the assessment reports to the *CIS Host Server* or configure the centralized script to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD).
6. Share the **CIS** folder as CIS.

The resulting directory structure should be as follows:

	- CIS\Assessor-CLI
	- CIS\Assessor-CLI\benchmarks
	- CIS\Assessor-CLI\config
	- CIS\Assessor-CLI\lib
	- CIS\Assessor-CLI\licenses
	- CIS\Assessor-CLI\misc
	- CIS\Assessor-CLI\reports
	- CIS\Assessor-CLI\sce
	- CIS\Assessor-CLI\scripts
	- CIS\Assessor-CLI\setup
	- CIS\Assessor-CLI\Assessor-CLI.jar
	- CIS\cis-cat-centralized.bat or CIS\cis-cat-centralized-ccpd.bat
	- CIS\Java
	- CIS\Java64
	- CIS\Reports

#### Security Considerations ####
The CIS\Reports folder will contain reports that detail configuration related vulnerabilities for each system evaluated by CIS-CAT. As such, “Authenticated Users” should **only** be granted “Write” and “List Folder Contents” access to the contents of this folder, and read access to the CIS\Reports folder should be restricted to only those personnel who are necessary to the appropriate functioning of the *CIS Host Server*:

![](https://i.imgur.com/wCMWpV1.png)

Permissions which should be applied within the **CIS** folder on the *CIS Host Server*:

|File or Folder                   |Permissions                                        |
|---------------------------------|---------------------------------------------------|
|CIS                              |Permissions on the shared folder                   |
|CIS\cis-cat-centralized.bat **or** CIS\cis-cat-centralized-ccpd.bat |**Execute** to “Authenticated Users” |
|CIS\Assessor-CLI (folder) |**List Folder Contents**, **Read**, and **Read & Execute** to "Authenticated Users" |
|CIS\Java (folder) |**Read** and **Read & Execute** to “Authenticated Users” |
|CIS\Java64 (folder) |**Read** and **Read & Execute** to “Authenticated Users” |
|CIS\Reports (folder) |**List Folder Contents** and **Write** to “Authenticated Users” |

Additionally, Write, Modify, Read and Execute permissions on the above resources should be limited to only those users necessary to the appropriate functioning of the *CIS Host Server*.

#### Update cis-cat-centralized.bat ####
Once the **CIS** folder is setup on the *CIS Hosting Server*, a few modifications must be made to either `cis-cat-centralized.bat` or `cis-cat-centralized-ccpd.bat`. If you want to write the assessment reports to the *CIS Host Server*, utilize the `cis-cat-centralized.bat` script and modify it as directed in this section.  If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD), skip this section and go to the **"Update cis-cat-centralized-ccpd.bat"** section, instead. 

	SET NetworkShare=\\NETWORK_SHARE\CIS
Replace `NETWORK_SHARE` with the fully qualified domain name or IP address of the CIS-CAT Host Server.

	SET JavaPath=Java\jre
	SET JavaPath64=Java64\jre
Note that the 32-bit and 64-bit JRE paths are those installed in step 4 under the **Create CIS Share on the CIS Hosting Server** section above.

	SET JavaMaxMemoryMB=768
Indicate the maximum amount of memory CIS-CAT will allocate for execution.  The default is 768 MB.  When executing with 32-bit versions of the JRE, this value can be set to a maximum of 2048 MB.  64-bit JRE’s may allocate as much memory as is required, limited by the available memory of machines invoking CIS-CAT.

	SET CisCatPath=Assessor-CLI
Set the CisCatPath value to the location, relative to the network share, of the installed version of CIS-CAT.  For example, the value above indicates the path to CIS-CAT is `\\NETWORK_SHARE\CIS\Assessor-CLI`.

	SET ReportsPath=Reports
Set the ReportsPath value to the location, relative to the network share, of the folder to which CIS-CAT reports are written.  For example, the value above indicates `\\NETWORK_SHARE\CIS\Reports` as the location to which reports are written.

	SET CISCAT_OPTS=-html -txt -csv
Finally, set the various reporting options to be used when launching CIS-CAT.

* `-html` indicates generation of the CIS-CAT XML report.
* `-txt` indicates generation of the CIS-CAT Text report.
* `-csv` indicates generation of the CIS-CAT CSV report.
* `-narf` indicates that CIS-CAT should NOT generate an Asset Reporting Format (ARF) report.

**Configuration Note:**  The “cis-cat-centralized.bat” script sets local environment variables denoting file system paths and folder names.  CIS recommends, for simplicity, that these paths do not contain spaces, as without modification to the script, spaces in paths can cause unexpected behavior.

Near line 780 of the “cis-cat-centralized.bat” script, the following code section illustrates the configuration of the CIS-CAT command-line for execution.

	Put all the options together and form the CIS-CAT command-line
	
	SET FULL_CISCAT_CMD=%mJavaPath%\bin\java.exe -Xmx%JavaMaxMemoryMB%M -jar %mCisCatPath%\Assessor-CLI.jar %CISCAT_OPTS% -b %mCisCatPath%\benchmarks\%Benchmark%
	
	ECHO	  Benchmark:	%Benchmark%
	ECHO	 Profile(s):	%Profiles%
	ECHO.
	ECHO Starting Assessment(s)...
	FOR %%P IN (%Profiles%) DO (
		ECHO  + %FULL_CISCAT_CMD% -p "%%P" -r "%mReportsPath%"
		ECHO  + Running Profile %%P...
		ECHO.
		ECHO [[ CIS-CAT ASSESSMENT START ]]
		IF %DEBUG%==1 ECHO CMDLINE = %FULL_CISCAT_CMD% -p "%%P" -r "%mReportsPath%" >> %DebugLogFile%
		%FULL_CISCAT_CMD% -p "%%P" -r "%mReportsPath%" 
		ECHO [[  CIS-CAT OUTPUT END  ]]
		ECHO.
	)

When spaces are included in any path names for environment variables, they must be surrounded with quotes to enable the full path to be discovered, for example:

	SET FULL_CISCAT_CMD=”%mJavaPath%\bin\java.exe” -Xmx%JavaMaxMemoryMB%M -jar “%mCisCatPath%\CISCAT.jar” -a 
	-s %CISCAT_OPTS% -b “%mCisCatPath%\benchmarks\%Benchmark%”

#### Update cis-cat-centralized-ccpd.bat ####
If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD) you have already setup, you must use the `cis-cat-centralized-ccpd.bat` file instead of the `cis-cat-centralized.bat` file.  Modify the `cis-cat-centralized-ccpd.bat` file as follows: 

	SET NetworkShare=\\CisHostServer\CIS
Replace `CisHostServer` with the fully qualified domain name or IP address of the CIS-CAT Host Server.

	SET JavaPath=Java\jre
	SET JavaPath64=Java64\jre
Note that the 32-bit and 64-bit JRE paths are those installed in step 4 under the **Create CIS Share on the CIS Hosting Server** section above.

	SET JavaMaxMemoryMB=768
Indicate the maximum amount of memory CIS-CAT will allocate for execution.  The default is 768 MB.  When executing with 32-bit versions of the JRE, this value can be set to a maximum of 2048 MB.  64-bit JRE’s may allocate as much memory as is required, limited by the available memory of machines invoking CIS-CAT.

	SET CisCatPath=Assessor-CLI
Set the CisCatPath value to the location, relative to the network share, of the installed version of CIS-CAT.  For example, the value above indicates the path to CIS-CAT is `\\NETWORK_SHARE\CIS\Assessor-CLI`.

	SET CCPDUrl=http://[YOUR-SERVER]/CCPD/api/reports/upload
Set the URL for the CIS-CAT Pro Dashboard API to which CIS-CAT assessment reports will be POST'ed.  The resource for CIS-CAT Pro Dashboard upload is **ALWAYS** mapped to the `/api/reports/upload` location, so the path to the application is all that should be modified here.  For example: http://applications.example.org/CCPD/api/reports/upload.

	SET CISCAT_OPTS=-nrf -ui
These options ensure only the ARF report file format is generated by the assessment process and SSL certificate warnings/errors are ignored when uploading the generated ARF assessment reports to the designated Dashboard.

	SET AUTHENTICATION_TOKEN=[Generate_An_Authentication_Token_In_CCPD]
Replace **[Generate_An_Authentication_Token_In_CCPD]** with the Authentication Token generated by an "API" user in the CIS-CAT Pro Dashboard to which the CIS-CAT assessment reports will be POST'ed to.


### Validate the Install ###
To test the setup, log into one of the target systems in the Workstation Group as a user capable of executing commands from an elevated command prompt, such as a domain admin.  Execute one of the following commands **from an elevated command prompt**, depending on which **.bat** file you intend to use (**cis-cat-centralized.bat** or **cis-cat-centralized-ccpd.bat**):

	C:\>\\CIS_HOST_SERVER\CIS\cis-cat-centralized.bat
	
	C:\>\\CIS_HOST_SERVER\CIS\cis-cat-centralized-ccpd.bat

Note that the **“CIS_HOST_SERVER”** value should be substituted with the actual name or IP of the machine configured as the CIS Host Server.

If successful, the above command will run an auto-assessment and result in output similar to the following:

![](https://i.imgur.com/7LV3Yce.png)

### Configuring the Scheduled Task via Group Policy ###
Perform the following steps to create and assign a Group Policy that will cause target systems in the Workstation Group to execute CIS-CAT via a Scheduled Task.  Note that some steps may vary slightly, depending on which version of Windows you are using.

1. Run `gpmc.msc` to modify the group policy
2. Select a group policy that is already targeted towards the computers that CIS-CAT needs to scan or create a new policy.
3. Next, create the scheduled task by navigating to **Computer Configuration -> Preferences -> Control Panel Settings -> Scheduled Tasks.**  Once there, click on **Action -> New -> Scheduled Task (Windows Vista and Later)**. Fill in the name of the task.
4. When setting the user who will be running the task, click the **“Change User or Group”** button, and click the **“Locations”** button on the **“Select User or Group”** popup:

    ![](https://i.imgur.com/KCdqvEZ.png)
1. On the **“Locations”** popup, expand the domain selection, select **“Builtin”** and click OK:

    ![](https://i.imgur.com/icaKMog.png)
1. Returning to the **“Select User or Group”** window, enter **“SYSTEM”** in the **“Enter the object name to select”** box, and click the **“Check Names”** button.  Select **“OK”** to select the SYSTEM user:

    ![](https://i.imgur.com/fLXSZlH.png)
    
    When returned to the scheduled task window, the **“NT AUTHORITY\System”** user should be indicated in the **“When running the task, use the following user account”** box.
1. Ensure the **“Run whether user is logged on or not”** radio button is selected, and make sure **“Run with highest privileges”** is checked.  It should look similar to the below screen shot.  Note that the **“Do not store password.  The task will only have access to local resources.”** checkbox will automatically be checked and disabled.  The inability to store credentials in the scheduled task is the result of applying the patch for **Microsoft security update MS14-025**.

    ![](https://i.imgur.com/0gtyt4M.png)
1. Add in whatever scheduling is needed via the **Triggers** tab.  Then go to the **Actions** tab click New and specify the following settings:
   * Set the **Action** drop down to **Start a program**
   * Set **Program/script** to **cmd.exe**
   * Set **Add arguments(optional)** to one of the following values, depending on whether you want to use the `cis-cat-centralized.bat` file **or** the `cis-cat-centralized-ccpd.bat` file.  Replace `<CisHostServer>` with the fully qualified domain name or IP address of the *CIS-CAT Host Server* you setup previously:

		`/c \\<CisHostServer>\CIS\cis-cat-centralized.bat`
	
		**or**
	
		`/c \\<CisHostServer>\CIS\cis-cat-centralized-ccpd.bat`

Once these steps are implemented, the **New Action** Dialog will look similar to the following:

![](https://i.imgur.com/AESSqVw.png)

Click **OK**.  CIS-CAT is now scheduled to run on all computers that are associated with the group policy.  The CIS-CAT assessment reports will be stored in the reports location or Dashboard you specified in the `cis-cat-centralized.bat` or `cis-cat-centralized-ccpd.bat` file, respectively.

### Bandwidth Considerations ###
Through the deployment and testing of the CIS-CAT Centralized workflow, bandwidth utilization can reach approximately 300 MB of data for each machine invoking CIS-CAT.  This bandwidth utilization is the cost of invoking CIS-CAT over the network.

## Assessing Multiple Unix/Linux Targets ##
Similar to the **“Assessing Multiple Windows Targets”** section above, it is possible to assess multiple Unix, Linux, MacOS, Debian, Solaris, SUSE, etc targets in an automated manner without installing CIS-CAT or the JRE on each target.  Either the `cis-cat-centralized.sh` script or the `cis-cat-centralized-ccpd.sh` script is intended to reside on a centralized file share (referred to as the *CIS Host Server* in this document) that is accessible by the computers to be assessed by CIS-CAT.  The choice of which of these two files to use depends on where the assessment reports are to be written.  If you want to send the assessment reports to a Reports folder on the *CIS Host Server*, then use the cis-`cat-centralized.sh` file.  If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD) you have already setup, you must use the `cis-cat-centralized-ccpd.bat` file instead.  See the **"Update cis-cat-centralized.sh"** and **"Update cis-cat-centralized-ccpd.sh"** sections that follow for more information.

### CIS Host Server ###
The *CIS Host Server* is where the CIS-CAT bundle (including the various Java Runtime Environments) and possibly the Reports are placed.  Configured target machines will access these resources to perform a self-assessment using CIS-CAT.

Using the default configuration, consider the root folder for this workflow to be located at `/cis`.  

1. The first setup step in setting up the *CIS Host Server* is to copy the required scripts to the root folder.  The four scripts which are required reside in the `
2. /Unix-Linux` folder of a CIS-CAT installation bundle:
   * cis-cat-centralized.sh **OR** cis-cat-centralized-ccpd.sh
   * detect-os-variant.sh
   * make-jre-directories.sh
   * map-to-benchmark.sh
1. The next step is to copy the `Assessor-CLI` folder, and its contents, contained in the unzipped bundle to the workflow's root folder.
2. The last step in setting up the *CIS Host Server* is to configure the JRE sub-folders. The **“cis-cat-centralized.sh”** and **“cis-cat-centralized-ccpd.sh”** scripts are configured with an option to create the **“jres”** subfolder and all OS-specific folders underneath it.  Run one of the following commands, depending on whether you are using the **“cis-cat-centralized.sh”** or the **“cis-cat-centralized-ccpd.sh”** script: 

	`/cis> ./cis-cat-centralized.sh --make-jre-directories`

	or

	`/cis> ./cis-cat-centralized-ccpd.sh --make-jre-directories`

The default configuration of the *CIS Host Server* folder structure should now be as follows:

	/cis

	/cis/Assessor-CLI
	/cis/Assessor-CLI/reports
	...

	/cis/cis-cat-centralized.sh OR /cis/cis-cat-centralized-ccpd.sh   <-- Copied from misc/Unix-Linux
	/cis/detect-os-variant.sh                                         <-- Copied from misc/Unix-Linux
	/cis/make-jre-directories.sh                                      <-- Copied from misc/Unix-Linux
	/cis/map-to-benchmark.sh                                          <-- Copied from misc/Unix-Linux
	
	/cis/jres
	/cis/jres/AIX
	/cis/jres/AIX/bin/java
	...
	/cis/jres/Debian
	/cis/jres/HPUX
	/cis/jres/Linux
	/cis/jres/OSX
	/cis/jres/RedHat
	/cis/jres/Solaris
	/cis/jres/SolarisSparc
	/cis/jres/SUSE

### Update cis-cat-centralized.sh ###
Once the *CIS Host Server* is setup, a few modifications must be made to either `cis-cat-centralized.sh` or `cis-cat-centralized-ccpd.sh`. If you want to write the assessment reports to the *CIS Host Server*, utilize the `cis-cat-centralized.sh` script and modify it as directed in this section.  If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD), skip this section and go to the **"Update cis-cat-centralized-ccpd.sh"** section, instead.

	CISCAT_DIR=/cis/Assessor-CLI
	REPORTS_DIR=/cis/Assessor-CLI/reports
	JRE_BASE=/cis/jres
CISCAT_DIR, REPORTS_DIR, and JRE_BASE should be configured to align with the *CIS Host Server* folder structure. 

	SSLF='0'
The script can be configured to execute either the **“Level 1”** or **“Level 2”** **profile** (if available), based on an environment variable value.  This variable is named `SSLF`, and may be set to either 0 or 1.  Setting the value to 0 results in CIS-CAT evaluating the "Level 1" profile, while setting the value to 1 results in CIS-CAT evaluating the “Level 2” profile.

### Update cis-cat-centralized-ccpd.sh ###
If you want to send the assessment reports directly to a CIS-CAT Pro Dashboard (CCPD) you have already setup, you must use the `cis-cat-centralized-ccpd.sh` file instead of the `cis-cat-centralized.sh` file.  Modify the `cis-cat-centralized-ccpd.sh` file as follows: 

	CISCAT_DIR=/cis/Assessor-CLI
	JRE_BASE=/cis/jres
CISCAT_DIR and JRE_BASE should be configured to align with the *CIS Host Server* folder structure. 

	CCPD_URL=http://[YOUR-SERVER]/CCPD/api/reports/upload
CCPD_URL is used to set the URL for the CIS-CAT Pro Dashboard API to which CIS-CAT assessment reports will be POST'ed.  The resource for CIS-CAT Pro Dashboard upload is **ALWAYS** mapped to the `/api/reports/upload` location, so the path to the application is all that should be modified here.  For example: http://applications.example.org/CCPD/api/reports/upload.

	AUTHENTICATION_TOKEN=[Generate_An_Authentication_Token_In_CCPD]
Replace **[Generate_An_Authentication_Token_In_CCPD]** with the Authentication Token generated by an "API" user in the CIS-CAT Pro Dashboard to which the CIS-CAT assessment reports will be POST'ed to.

	SSLF='0'
The script can be configured to execute either the **“Level 1”** or **“Level 2”** **profile** (if available), based on an environment variable value.  This variable is named `SSLF`, and may be set to either 0 or 1.  Setting the value to 0 results in CIS-CAT evaluating the "Level 1" profile, while setting the value to 1 results in CIS-CAT evaluating the “Level 2” profile.

### Validate the Install ###
To test the setup, log into one of the target systems that has access to the *CIS Host Server* as either a root user or a user capable of executing commands using sudo.  Execute one of the following commands, depending on which **.sh** file you intend to use (**cis-cat-centralized.sh** or **cis-cat-centralized-ccpd.sh**):

	> /path/to/cis/cis-cat-centralized.sh

	or
	
	> /path/to/cis/cis-cat-centralized-ccpd.sh

Note that `/path/to/cis` represents the file system path to the *CIS Host Server* and should be modified as appropriate before running the command.

If successful, the above command will run an auto-assessment on the target system and indicate successfully completion of the assessment.

The CIS-CAT assessment reports will be stored in the reports location or Dashboard you specified in the `cis-cat-centralized.sh` or `cis-cat-centralized-ccpd.sh` file, respectively.

CIS-CAT users can now integrate the invocation of the **“cis-cat-centralized.sh”** or **“cis-cat-centralized-ccpd.sh”** script into a task scheduling system such as `cron`, to be executed on any schedule deemed prudent for organizational needs.  Configuration of a Unix/Linux-based scheduling tool is beyond the scope of this User’s Guide.

## Exit Codes ##
A number of scenarios exist which could cause CIS-CAT Pro Assessor to terminate prior to completing its work.  Various errors could occur, such as the inability to ingest assessment content, session connectivity problems, etc.  The following table describes the set of CIS-CAT Pro Assessor's exit codes:

| Exit Code | Description                                                              |
|-----------|--------------------------------------------------------------------------|
|0          | CIS-CAT Pro Assessor Exited Successfully.                                |
|100        | Invalid starting directory                                               |
|101        | No valid assessment content was found.                                   |
|102        | CIS-CAT Pro Assessor could not find custom properties file.              |
|103        | CIS-CAT Pro Assessor could not parse custom properties.                  |
|104        | CIS-CAT Pro Assessor could not find custom session properties file.      |
|105        | CIS-CAT Pro Assessor could not find the specified OVAL Definitions file. |
|106        | CIS-CAT Pro Assessor could not find the specified OVAL Variables file.   |
|107        | CIS-CAT Pro Assessor encountered invalid assessment content.             |
|108        | CIS-CAT Pro Assessor could not find Benchmark content.                   |
|109        | CIS-CAT Pro Assessor encountered an invalid data-stream.                 |
|110        | CIS-CAT Pro Assessor encountered an invalid checklist.                   |
|111        | CIS-CAT Pro Assessor encountered an invalid profile.                     |
|112        | CIS-CAT Pro Assessor encountered an invalid interactive value.           |
|113        | CIS-CAT Pro Assessor could not parse an XML file required for assessment.|
|114        | CIS-CAT Pro Assessor could not find an XML file required for assessment. |
|115        | An XML file was parsed but contained an invalid XML Signature.           |
|116        | Process not executing with elevated privileges.  When executing the Assessor in "host-based" mode (using a "local" session only), it must be launched with elevated privileges.  When executing on Windows, this requires the user to launch a command prompt "As an Administrator".  When executing on any Unix or Linux OS, the user must either be logged in as `root` or have the ability to launch the Assessor using `sudo`.                        |
|117        | CIS-CAT Pro Assessor could not encrypt a sessions or configuration file. |
|118        | A required command line option for encrypting a sessions or configuration file was missing.          |
|119        | CIS-CAT Pro Assessor could not decrypt a sessions or configuration file. |
|500        | An XML file was parsed but XML Schema validation errors.                 |


## Troubleshooting and Support ###
CIS-CAT Pro Assessor v4 is generally available, and member support is available through the normal CIS SecureSuite channels:

- Email support at [support@cisecurity.org](mailto:support@cisecurity.org)
- Start a discussion on the [CIS-CAT Discussion Group](https://workbench.cisecurity.org/communities/30) (login required)
