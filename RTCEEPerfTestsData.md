META:TOPICINFO{author="jdiaz" date="1409568288" format="1.1"
reprev="1.2" version="1.2"}
META:TOPICPARENT{name="RTCSystemZPerformanceTesting"}
STARTSECTION{"Intro"} This section describes the data that is used for
the performance tests that are specific for the Enterprise Extensions
features tests scenarios. The data is based on a sample application
which, to achieve levels that will allow us to test scalability of the
solution, is replicated generating several different variations. The
base application used as data for the testing is the [Mortage
Application](https://jazz.net/wiki/pub/Main/ZOSBuildSamplesV4/MortgageApplication.zip).
This sample application is included as part of the Money That Matters
sample. The application contains **5 (five)** zComponent projects with
the following base assets relevant numbers:

Element Type \# Elements Size Average size Max size

COBOL program 6 165KB 27.5KB 133KB

Copybook 6 3KB 0.5KB 568 bytes

REXX 2 2.6KB 1.3KB 1.3KB

BMS 2 9KB 4.5KB 6.5KB

Link Card 1 0.5KB 0.5KB 0.5KB

BIND file 2 0.8KB 0.4KB 492 bytes

The sample application is a COBOL/CICS application that has a number of
both statically called programs and dynamically called programs with a
number of common and module specific copybooks. The process flow of the
application from a CICS perspective is as follows:

1.  Users starts the application by issuing the EPSP transaction and
    this runs the EPSCMORT program.
2.  EPSCMORT statically calls EPSNBRVL to perform number validation
3.  EPSCMORT dynamically calls EPSCSMRT via an EXEC CICS LINK to pass
    parameters to the mortgage payments program
4.  EPSCMORT dynamically calls EPSMLIST when PF9 is pressed to display a
    list of records from a file
5.  EPSCSMRT dynamically calls EPSMPMT via an EXEC CICS LINK to
    calculate the mortgage payment

ENDSECTION{"Intro"}

### Scalability Test Data

The following data is generated automatically based on the described
sample application data. Automatic volume generation is achieved by
replication of source code elements obtaining the following sets of test
data:

##### MortgageApplicationx10 STARTSECTION{"Mortx10"} [mortgageapplicationx10-startsectionmortx10]

10 times replication of [Mortage
Application](https://jazz.net/wiki/pub/Main/ZOSBuildSamplesV4/MortgageApplication.zip)
sample.

Assets Overall dev assets

60 COBOL programs 40 Copybooks 20 BMS 3 others 123

ENDSECTION{"Mortx10"}

##### MortgageApplicationx100 [mortgageapplicationx100]

STARTSECTION{"Mortx100"} 100 times replication of [Mortage
Application](https://jazz.net/wiki/pub/Main/ZOSBuildSamplesV4/MortgageApplication.zip)
sample.

Assets Overall dev assets

600 COBOL programs 400 Copybooks 200 BMS 3 others 1203

ENDSECTION{"Mortx100"}

##### MortgageApplicationx250 [mortgageapplicationx250]

STARTSECTION{"Mortx250"} 250 times replication of [Mortage
Application](https://jazz.net/wiki/pub/Main/ZOSBuildSamplesV4/MortgageApplication.zip)
sample.

Assets Overall dev assets

1500 COBOL programs 1000 Copybooks 500 BMS 3 others 3003

ENDSECTION{"Mortx250"}

##### MortgageApplicationx500 [mortgageapplicationx500]

STARTSECTION{"Mortx500"} 500 times replication of [Mortage
Application](https://jazz.net/wiki/pub/Main/ZOSBuildSamplesV4/MortgageApplication.zip)
sample.

Assets Overall dev assets

3000 COBOL programs 2000 Copybooks 1000 BMS 3 others 6003

ENDSECTION{"Mortx500"}

##### MortgageApplicationx1000 [mortgageapplicationx1000]

STARTSECTION{"Mortx1000"} 1000 times replication of [Mortage
Application](https://jazz.net/wiki/pub/Main/ZOSBuildSamplesV4/MortgageApplication.zip)
sample.

Assets Overall dev assets

6000 COBOL programs 4000 Copybooks 2000 BMS 3 others 12003

ENDSECTION{"Mortx1000"} These sets of data are used in different tests
to be able to reproduce different conditions and volumes of information.
