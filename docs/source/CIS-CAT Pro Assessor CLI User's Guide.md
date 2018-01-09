![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor CLI User's Guide #

## Introduction ##
The CIS-CAT Pro Assessor CLI is a command-line user interface, allowing users to assess target systems against various forms of machine-readable content.  CIS-CAT Pro Assessor CLI is designed primarily to assess CIS Benchmark configuration recommendations but can also assess content written in conformance with the Security Content Automation Protocol (SCAP), as well as plain OVAL definition content.

## Remote Assessment Capability ###
Arguably the most important feature to be included in CIS-CAT Pro Assessor v4 is the ability to assess remote endpoints.  Providing appropriate connection information allows CIS-CAT Pro Assessor to establish a "session", execute commands, run scripts, and perform collection and evaluation for the remote endpoint.  For Microsoft Windows endpoints, this "session" is established through the use of WinRM.  For Unix/Linux and Cisco network device endpoints, CIS-CAT Pro Assessor establishes the "session" via SSH.

Endpoints to be assessed must be configured appropriately to allow for remote access.  Please see the [CIS-CAT Pro Assessor Configuration Guide](./ciscat-pro-assessor-configuration-guide.html) for more information.

## Deployment ##
CIS-CAT Pro Assessor CLI is a simple Java-based application and as such, requires a Java Runtime Environment (JRE) at or above version 1.8, in order to execute.  A suitable JRE may be installed to the machine on which CIS-CAT is installed, or may be located on a network share.  As long as the machine executing the CIS-CAT Pro Assessor CLI application can access a suitable JRE, it may be used to run the tool.

## Using CIS-CAT Pro Assessor CLI ##
Bundled with the application are two script files; a Microsoft Windows batch script, `Assessor-CLI.bat` and a Unix/Linux shell script, `Assessor-CLI.sh`.  These scripts serve as the entry point to the application.  Any examples included in this user's guide will utilize the Microsoft Windows batch script, but usage of the Unix/Linux shell script can be substituted.

## Command Line Options ##
CIS-CAT Pro Assessor CLI can perform a variety of functions related to both benchmark and vulnerability assessments.  The myriad command-line options allow for combined usage to initiate these functions.

### Basic Options ###

Basic operation of CIS-CAT Pro Assessor CLI allows a user to get help, list available content, or to interactively step through the selection of a benchmark and profile prior to executing an assessment.

| Short Option  | Long Option   |  Argument(s)      | Description                    |
| ------------- | ------------- | ------------|---------------------------------- |
| `-h`          | `--help`      | N/A | Display CIS-CAT Pro Assessor help output. |
| `-l`          | `--list`      | N/A | List the benchmarks available for assessment.|
| `-v`          | `--verbose`   | N/A |Enable more verbose output when combined with the `-l` option, specifically displaying the full filepath to the benchmark, for later assessment using the `-b` option.|
| `-i`          | `--interactive` | N/A | Execute the Assessor in "interactive" mode specifically for benchmark assessments, allowing the user to manually select a benchmark and profile for assessment.  Based on the selected benchmark, the user may be required to enter "interactive values" which are then used by the assessment engine. |
| `-o`          | `--definitions` | N/A | Execute the Assessor in "interactive" mode specifically for the manual selection and evaluation of OVAL Definitions files, and (optionally) selecting and associating an OVAL Variables file as well.|
| `-d`          | `--startingDir` | `<DIRECTORY>` | Configure the relative root folder from which other options, such as benchmarks, can be found. |

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


### Benchmark/Data-Stream Collection Options ###
The benchmark and data-stream collection options provide users the ability to select specific content for assessment.  The `-b` option gives the user the choice to specify the path to either the XCCDF file (containing the `<Benchmark>` element) or the Data-stream collection file.  Using the `-p` option, users can select a specific configuration profile to assess, using either the profile's ID or the profile's title/name.

| Short Option  |  Long Option  |   Argument   | Description                      |
| ------------- | ------------- | -------------|--------------------------------- |
| `-b`          | `--benchmark` | `<BMK-OR-DSC>` | Specify either the full filepath to the assessment content or a path relative to the starting directory.  The `<BMK-OR-DSC>` argument represents either a Benchmark XCCDF file, or the SCAP 1.2-formatted Data-stream Collection file.|
| `-ds`         | `--data-stream` | `<DATA-STREAM>` | Used only when the `-b` option selects a data-stream-collection document, the `-ds` option specifies, within the collection, the ID of the data-stream to be assessed. |
| `-cl` | `--checklist` | `<CHECKLIST>` | Used only in conjunction with the `-ds` option, the `-cl` option specifies, within the data-stream, the ID of the checklist (benchmark) to be assessed.|
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

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -ds scap_org.cisecurity_datastream_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using a specific data-stream, a specific checklist, and the default first profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -ds scap_org.cisecurity_datastream_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark -cl xccdf_org.cisecurity.benchmarks_benchmark_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using a specific data-stream, a specific checklist and a specific profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -ds scap_org.cisecurity_datastream_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark -cl xccdf_org.cisecurity.benchmarks_benchmark_1.0.0_CIS_Microsoft_Windows_Server_2016_Benchmark -p "Level 1 - Member Server"


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


### Miscellaneous Options ###

| Short Option  |   Long Option   |    Argument   | Description                       |
| ------------- | --------------- | --------------|---------------------------------- |
| `-vdd` | `--vulnerability-definitions` | N/A | Download the latest supported vulnerability definitions information for the supported platforms: Microsoft Windows, Red Hat Linux, SuSE Enterprise Linux, and Ubuntu|
| `-sessions`| `--sessions`| `<SESSIONS.PROPERTIES>`| The `-sessions` option allows users to configure multiple endpoints for assessment of a benchmark.  The `sessions.properties` file configures CIS-CAT Pro Assessor for the assessment of remote endpoints by specifying remote hosts, ports, and credentials which the application will use for connection, collection and evaluation of benchmark recommendations and/or vulnerabilities.  See "Remote Assessment Capability" below for more information.  <br/><br/>If no `sessions.properties` file exists or no connections are configured in the file, CIS-CAT Pro Assessor CLI will assess the local machine.|
| `-props`| `--properties`| `<PROPERTIES-FILE>`| The CIS-CAT Pro Assessor CLI user properties file defaults many runtime properties used during the assessment process.  These properties may be customized per assessment or per endpoint, by creating individual properties files, and specifying either the full filepath or a path relative to the working directory.|
| `-D`| N/A| `<Property=Value>`| Instead of creating a new properties file for unique assessments, individual user properties may be specified using the `-D` option together with a `property=value` pair.  This allows an assessment to only override specific user properties when only a small number differ from the defaults.|

#### Examples ####
Download the latest vulnerability definitions:

	> Assessor-CLI.bat -vdd

Execute an assessment against the CIS Microsoft Windows 10 benchmark, using the relative path to the benchmark file, automatically selecting the first profile, assessing a number of remote machines, configured in a specific session configuration file:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -sessions C:\CIS\sessions\windows_10_machines.properties


Execute an assessment against the CIS Oracle Database 11g R2 benchmark, selecting the Windows Server Host OS profile, and configuring the required "interactive" values:

	> Assessor-CLI.bat -b benchmarks\CIS_Oracle_Database_11g_R2_Benchmark_v2.2.0-xccdf.xml -p "Level 1 - Windows Server Host OS" -D xccdf_org.cisecurity_value_jdbc.url=jdbc:oracle:thin:user/s3cr3t@DBHOST:1521:devdb -D xccdf_org.cisecurity_value_listener.ora=C:\product\oracle\network\admin\listener.ora


## Troubleshooting and Support ###
Member support for CIS-CAT Pro Assessor is available through the normal support channels:

- Email support at [support@cisecurity.org](mailto:support@cisecurity.org)
- Start a discussion on the [CIS-CAT Discussion Group](https://workbench.cisecurity.org/communities/30) (login required)
