![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor CLI User's Guide #

## Introduction ##
The CIS-CAT Pro Assessor CLI is a command-line user interface, allowing users to assess target systems against various forms of machine-readable content.  CIS-CAT Pro Assessor CLI is designed primarily to assess CIS Benchmark configuration recommendations but can also assess content written in conformance with the Security Content Automation Protocol (SCAP), as well as plain OVAL definition content.

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

Execute an assessment of a benchmark/data-stream in "interactive" mode:

	> Assessor-CLI.bat -i

Execute an assessment of a benchmark/data-stream in "interactive" mode, selecting a benchmark from a location relative to a specific folder:

	> Assessor-CLI.bat -i -d C:\CIS\My-Benchmarks

Execute an assessment of an OVAL Definitions file in "interactive" mode:

	> Assessor-CLI.bat -i -o

Execute an assessment of an OVAL Definitions file in "interactive" mode, selecting the definitions file from a location relative to a specific folder:

	> Assessor-CLI.bat -i -o -d C:\CIS\My-Benchmarks


### Benchmark/Data-Stream Collection Options ###
| Short Option  |  Long Option  |   Argument   | Description                      |
| ------------- | ------------- | ----------------------------------------------- |
| `-b`          | `--benchmark` | `<BENCHMARK>` | Specify either the full filepath to a benchmark XML file (an XCCDF), or a path relative to the starting directory. |
| `-ds`         | `--data-stream` | `<DATA-STREAM>` |  |
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

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -ds

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using a specific data-stream, a specific checklist, and the default first profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -ds

Execute an assessment against the CIS Microsoft Windows Server 2016 data-stream collection, using a specific data-stream, a specific checklist and a specific profile:

	> Assessor-CLI.bat -b benchmarks\CIS_Microsoft_Windows_Server_2016_Benchmark_v1.0.0-datastream.xml -ds


### OVAL Definitions Assessment Options ###
| Short Option  |  Long Option  |   Argument   | Description                      |
| ------------- | ------------- | -------------|--------------------------------- |
| `-od     ` | `--oval-definitions` | `<OVAL_DEFINITIONS>` | Specify either the full filepath to an OVAL Definitions XML file, or a path relative to the starting directory.|
| `-ov` | `--oval-variables` | `<OVAL_VARIABLES>` | Only used in conjunction with the `-od` option, the `-ov` option specifies either the full filepath to an OVAL Variables XML file, or a path relative to the starting directory.|

#### Examples ####


### Reporting Options ###
A number of options exist for generating assessment results.  When a benchmark or data-stream collection is assessed, the Asset Reporting Format (ARF) results are generated.  The ARF report is an XML document containing Asset Information for the endpoint under assessment, the benchmark/data-stream that was assessed, system characteristics, and assessment results.  When OVAL Definitions are assessed, an "OVAL results with system characteristics" XML document is produced by default.  These reports are automatically generated and cannot be disabled.  These XML documents are designed to be either uploaded directly to CIS-CAT Pro Dashboard, or transformed into more human-readable HTML, CSV or plain-text documents.

The following table summarizes a number of options controlling which reports to generate, naming of reports, and functionality allowing users to upload reports to a URL, such as CIS-CAT Pro Dashboard.

| Short Option  |   Long Option   |    Argument   | Description                        |
| ------------- | --------------- | --------------|----------------------------------- |
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


### Extra configuration Options ###

	-sessions, --sessions <SESSIONS.PROPERTIES>
The `-sessions` option allows users to configure multiple endpoints for assessment of a benchmark.  The `sessions.properties` file configures CIS-CAT Pro Assessor for the assessment of remote endpoints by specifying remote hosts, ports, and credentials which the application will use for connection, collection and evaluation of benchmark recommendations and/or vulnerabilities.  See "Remote Assessment Capability" below for more information.

If no `sessions.properties` file exists or no connections are configured in the file, CIS-CAT Pro Assessor CLI will assess the local machine.

	-props, --properties <PROPERTIES-FILE>
The CIS-CAT Pro Assessor CLI user properties file defaults many runtime properties used during the assessment process.  These properties may be customized per assessment or per endpoint, by creating individual properties files, and specifying either the full filepath or a path relative to the working directory.

	-D <Property=Value>
Instead of creating a new properties file for unique assessments, individual user properties may be specified using the `-D` option together with a `property=value` pair.  This allows an assessment to only override specific user properties when only a small number differ from the defaults.

### Debugging Options ###
	-v, --verbose
Enable more verbose output when combined with the `-l` option.

----------

## Remote Assessment Capability ###

### Producing Reports ###

### Examples ###
The following are common examples for executing CIS-CAT Pro Assessor CLI.  Note the `>` indicates a command prompt.
#### List All Available Benchmarks ####
    > java -Xmx768m -jar Assessor-CLI-1.0.0.jar -l

#### List All Available Benchmarks (with `-b` information)
    > java -Xmx768m -jar Assessor-CLI-1.0.0.jar -l -v

#### Execute interactively against the local host ####
    > java -Xmx768m -jar Assessor-CLI-1.0.0.jar -i

#### Configure Sessions ####
    > java -Xmx768m -jar Assessor-CLI-1.0.0.jar -sessions config\windows.properties

#### Assess a specific benchmark and profile ####
    > java -Xmx768m -jar Assessor-CLI-1.0.0.jar -b benchmarks\CIS_Microsoft_Windows_10_Enterprise_Release_1703_Benchmark_v1.3.0-xccdf.xml -p "Level 1"

#### Download Vulnerability Definitions ####
    > java -Xmx768m -jar Assessor-CLI-1.0.0.jar -vdd

#### Execute a Vulnerability Assessment ####
    > java -Xmx768m -jar Assessor-CLI-1.0.0.jar -od vulnerabilities\microsoft_windows_10.xml

