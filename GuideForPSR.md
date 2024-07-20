META:TOPICINFO{author="amano" date="1395897874" format="1.1"
reprev="1.1" version="1.1"}
META:TOPICPARENT{name="DataCollectionandSupportResources"}

# Guideline of using "Problem Steps Recorder" [guideline-of-using-problem-steps-recorder]

DKGRAY Authors: Main.TakehikoAmano Build basis: None ENDCOLOR

TOC{title="Page contents"}

There is a utility called "Problem Steps Recorder" on Windows　7 and 8.
This utility records application operations with automatic GUI screen
capture. This is useful to report the problem to IBM support team so
that they can understand the problems, and how to reproduce the problem.

## Using Problem Steps Recorder

To use this tool is very simple.

1\. Enter "psr" at "Start" -\> "Run...", or run this utility from
command line interface.

2\. Press "Start Record"

-   PSR start recording:

3\. Run the application to reproduce the problem. Optionally, you may
enter comment during the capture.

4\. Press "Stop Record". The dialog will pop up to save the recording.

-   PSR stop recording:

The record is saved as .zip file which contains self-contains .mht file.

## Before sending the file

The "psr" utility do not capture input. You may need to supply
additional comment to the file (or enter comment during the capture).
Make sure the captured screenshots are correct before sending to IBM. If
it contains confidential information, be sure to mask the information.

##### External links: [external-links]

-   [Microsoft site about using psr
    utility](http://windows.microsoft.com/en-us/windows7/how-do-i-use-problem-steps-recorder)

META:FILEATTACHMENT{name="psr-start-recording.png"
attachment="psr-start-recording.png" attr="" comment="PSR start
recording" date="1395897513" path="psr-start-recording.png" size="18581"
user="amano" version="2"}
META:FILEATTACHMENT{name="psr-stop-recording.png"
attachment="psr-stop-recording.png" attr="" comment="PSR stop recording"
date="1395897285" path="psr-stop-recording.png" size="14345"
user="amano" version="1"}
