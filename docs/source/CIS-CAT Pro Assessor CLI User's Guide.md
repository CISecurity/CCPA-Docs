![](http://i.imgur.com/5yZfZi5.jpg)

# CIS-CAT Pro Assessor User's Guide #

## Introduction ##
The CIS-CAT Pro Assessor is a command-line user interface, allowing users to assess target systems against various forms of machine-readable content.  CIS-CAT Pro Assessor is designed primarily to assess CIS Benchmark configuration recommendations but can also assess content written in conformance with the Security Content Automation Protocol (SCAP), as well as plain OVAL definition content.

## Deployment ##
CIS-CAT Pro Assessor is a simple Java-based application and as such, requires a Java Runtime Environment (JRE) at or above version 1.8, in order to execute.  A suitable JRE may be installed to the machine on which CIS-CAT is installed, or may be located on a network share.  As long as the machine executing the CIS-CAT Pro Assessor application can access a suitable JRE, it may be used to run the tool.

## Using CIS-CAT Pro Assessor ##

### Command Line Options ###
CIS-CAT Pro Assessor CLI can perform a variety of functions related to both benchmark and vulnerability assessments.  The myriad command-line options allow for combined usage to initiate these functions.

- Basic Options
`-h, --help`: Display CIS-CAT Pro Assessor help output.
`-l, --list`: List the benchmarks available for assessment.
`-i, --interactive`: Execute the Assessor in "interactive" mode specifically for benchmark assessments, allowing the user to manually select a benchmark and profile for assessment.  Based on the selected benchmark, the user may be required to enter "interactive values" which are then used by the assessment engine.
`-o, --definitions`: Execute the Assessor in "interactive" mode specifically for the manual selection and evaluation of OVAL Definitions files, and (optionally) selecting and associating an OVAL Variables file as well.

- Report Configuration Options
`-d, --startingDir`:  Configure the Assessor's starting directory.  When not used, the starting directory defaults to the folder location of the main Assessor .jar file.
`-rd, --reports-dir`: Configure the report destination folder, allowing users to configure the location to which result reports are written.
`-rp, --report-prefix`: 

- Benchmark/Data-Stream Collection Options
`-b, --benchmark <BENCHMARK>`:
`-ds, --data-stream <DATA-STREAM>`:
`-cl, --checklist <CHECKLIST>`:
`-p, --profile <PROFILE>`:

- OVAL Definitions Assessment Options:
`-od, --oval-definitions <OVAL_DEFINITIONS>`:
`-ov, --oval-variables <OVAL_VARIABLES>`:

- Extra configuration Options:
`-sessions, --sessions <SESSIONS.PROPERTIES>`:
`-props, --properties <PROPERTIES-FILE>`:
`-D <Property=Value>`:

- Report Generation Options
`-u, --url <REPORTS-URL>`: Specify a URL to which Assessor results are uploaded, using HTTP(S) POST.
`-ui, --ignore-warnings`:  Indicate that, when uploading results to a URL via the `-u` option, any SSL certificate warnings should be ignored.
`-nrf, --no-report-file`: This option disables generation of a results report file.  When utilizing the `-u` option, Assessor results are uploaded to the supplied URL.  In that use-case, report files are generally not needed.  

- Debugging Options:
`-v, --verbose`: Enable verbose debug logging.
``:
``:
``:
``:
``:
``:
``:

### Remote Assessment Capability ####

### Producing Reports ###

### Examples ###
List All Available Benchmarks
Execute interactively against the local host
Configure Sessions
Assess a specific benchmark and profile
Download Vulnerability Definitions
Execute a Vulnerability Assessment


