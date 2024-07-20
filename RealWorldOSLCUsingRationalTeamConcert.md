META:TOPICINFO{author="ralphe" date="1389630031" format="1.1"
reprev="1.4" version="1.4"}
META:TOPICPARENT{name="DeploymentIntegrating"}

# Real world OSLC using Rational Team Concert [real-world-oslc-using-rational-team-concert]

DKGRAY Authors: Glenn Bardwell, IBM Jazz L3,Richard Rakich, IBM
Architect/Project Lead Build basis:Rational Team Concert 4.0 ENDCOLOR

TOC{title="Page contents"}

[Open Services for Lifecycle Collaboration](http://open-services.net/)
(OSLC) is a technology that allows software lifecycle tools to share
data. RTC applications communicate via OSLC. Why should this be
important to you?

Below is a real world example of Rational's use of OSLC to integrate
customer support data into Rational Team Concert. The project, called
Rational OSLC Client Request (ROCR), is typical of the kind of product
integrations that are possible with OSLC.

## Background

Rational ClearQuest, is a highly configurable bug tracking system. It is
used in internally in Rational, to manage Customer Support data APARs
and other customer facing assets. Retain is a legacy CRM system used to
manage customer data.

ClearQuest integrates with Retain via the Retain bridge. Rational
Customer support enters customer names into Retain. Customer names are
pulled into ClearQuest via the Retain Bridge, a software interface
between Retain and ClearQuest.

Rational CLM (RTC, RQM, RRC, etc) is used internally in Rational to
manage source code, defects, enhancements, and other development
artifacts.

## ROCR requirements

The earlier version of the Rational RTC Escalation record included a
customer name, which was typed into the Escalation by the author. There
was no way to guarantee that the name was the same across all
Escalations. This made it difficult to track and report on issues common
to a customer.

In ROCR the requirements are more stringent. The Escalation author is
required to select the customer name from a list. The names also can't
be hard-wired into the ROCR escalation record. That would require too
much administrative overhead. There had to be a way to dynamically
update RTC with new customer data as it became available.

## Solution

ROCR uses the the ClearQuest OSLC interface to run queries against
ClearQuest. The ROCR team created batch files that run periodically,
extract data from ClearQuest and then write the data to XML files.

The ROCR team created a new WorkItem type: Escalation. In the Escalation
record, the ROCR team added new attributes whose values are read from
the web. The ROCR team pointed RTC to a web server that served up the
XML.

### Converting Retain data to XML

The ROCR team set up two batch/Perl programs that run periodically and
query ClearQuest. Here's how they work.

#### Product name batch program

The first batch program gets the list of products that are available to
customers. ClearQuest stores this data in a `Product` record type

Below are a list of the parameters that can be passed to the batch
program. The credentials can be passed explicitly or through a named
file.

-cquser The ClearQuest user Id

-cqpassword The ClearQuest password

-cqprojectarea The project area is the CQ Schema name. Default value:
CQPAR

-recordtype The record type to query on. Default value: Product

Note that it depends on the Lyo OSLC perl library. See Lyo Perl library,

The first step in the script is to log into ClearQuest. The Perl code
handles login, and the ROCR administrator supplies the credentials.

my \$CQ = Lyo::OSLC::CQ::CM-\>new; \$opt{cqurl} =
'<https://l2l3-cmn-cq.ratl.swg.usma.ibm.com/cqweb/oslc>'
\$CQ-\>credentials(\$opt{'cquserid'}, \$opt{'cqpassword'});
\$CQ-\>setBaseURI(\$opt{'cqurl'});

Once the ClearQuest (CQ) object is created from a URL and credentials,
the Perl code runs a query against CQ. Below is the query that extracts
the list of product names of from ClearQuest. The code removes
duplicates and sorts the results.

my @query = (qq(dcterms:type="Product")); my \$rdf =
\$cqclient-\>oslcWhere(\$opt{'cqprojectarea'}, \$opt{recordtype},
\$query, \\props); my \$records = \$rdf-\>QueryResults(); foreach my
\$record (@\${records}) { if (! (scalar grep \$record-\>{'cq:Product'}
eq \$\_ , @prodnames) ) { push(@prodnames, \$record-\>{'cq:Product'});
push(@result, { 'Product' =\> "\$record-\>{'cq:Product'}", }); } } my
@sorted = sort { lc(\$a-\>{'Product'}) cmp lc(\$b-\>{'Product'}) }
@result; \# alphabetical sort

Finally the data is written out to an XML file.

open( my \$fh, "\>/ROCRProdList.xml" ) or die "cannot open
/ROCRProdList.xml: \$"; my \$xml = XMLout( \\sorted, 'NoAttr' =\> 1,
'RootName' =\> 'xml', ); \$xml =\~ s/anon/node/g; print \$fh \$xml;
close(\$fh);

#### Customer name batch program

A second batch program builds a list of customers names. In Rational,
customer names are kept in a ClearQuest record called a RETAIN_PMR. The
code for this program is similar to the code that reads the product
list, with differences in the `record type` and `query` fields.

my @query = (qq(dcterms:type="RETAIN*PMR")); my @props = (
'cq:customerName', 'cq:customerNumber', ); my \$rdf =
\$cqclient-\>oslcWhere(\$opt{'cqprojectarea'},\$opt{recordtype},
\$query, \\props); my \$records = \$rdf-\>QueryResults(); foreach my
\$record (@\${records}) { if (! (scalar grep
\$record-\>{'cq:customerNumber'} eq \$* , @custnums) ) { push(@custnums,
\$record-\>{'cq:customerNumber'}); push(@result, { 'customerName' =\>
"\$record-\>{'cq:customerName'} \\\$record-\>{'cq:customerNumber'}\\",
'customerNumber' =\> "\$record-\>{'cq:customerNumber'}", }); } }

The batch program create two files, one containing the list of customer
products and a second containing the list of customer names and numbers.
Here is what they look like:

ClearCase

Rational Team Concert

RTC Customer 12345

Acme Corp 67890

### Serving up the XML

The ROCR team set up Apache Web Server to serve the XML files. To see
this yourself, download Apache Web Server. Store the XML data in
ROCRProdList.xml in the htdocs directory. Point your browser to
<http://localhost/ROCRProdList.xml>, and you should see the file.

### Updating the XML File

The ROCR team set up cron to periodically run the batch files. On
windows the at command runs jobs periodically (see at -help from the
MS-dos command line), On Linux, the cron command runs jobs periodically.

### RTC integration

The ROCR team used RTC HTTP Value Set Providers to dynamically build
content for dropdowns and pickers in the ROCR Escalation record.

See Customization of Work Items in Rational Team Concert, for for more
details on RTC customization. The ROCR team created a customized
WorkItem Type, `Escalation`, which includes two custom attributes:
`Product Name` and `Customer Name`. Under Attribute Customization, they
created two new HTTP Filtered Value Sets.

com.ibm.rational.escalation.attr.cust.customerName and
com.ibm.rational.escalation.attr.cust.productList.

The Filtered Value set user interface provides a mechanism for parsing
the XML to extract the relevant fields and recall the data.

**Customization**

ClearCase

Rational Team Concert

RTC Customer 12345

Acme Corp 67890

In the customization examples, the ROCR team retrieved the data inside
of the `product` and `customerName` tags. XPath provides a way to get
that data.

### Some background on using XPath

Imagine you're a ROCR developer looking trying to determine what values
to put in the Attribute Customization. You have a customer XML file. If
you think of the XML as a table where each row is a node, then to
describe an arbitrary row in this table, you'd select ./xml/node. An
example of a row is:

Acme Corp 67890

To extract the customerName column from the row, you would select a
Column XPath expression of ./customerName. Finally, to present the
result, you would select an Entry label format of \${0}.

The ROCR team used a Value Set Picker to present customer names, because
there are too many names to list in a dropdown. The product list is
smaller, so the ROCR team used a ValueSet Combo.

Putting it all together, the following figure shows a ROCR Escalation
record that displays a product list.

##### Related topics: [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home]

##### External links: [external-links]

-   [IBM](https://www.ibm.com)

##### Additional contributors: Main.TWikiUser [additional-contributors-main.twikiuser]

META:FILEATTACHMENT{name="architecture.png"
attachment="architecture.png" attr="h" comment="" date="1386966195"
path="architecture.png" size="8622" user="gbardwel" version="1"}
META:FILEATTACHMENT{name="rocrproduct.png" attachment="rocrproduct.png"
attr="h" comment="" date="1386966737" path="rocrproduct.png"
size="33037" user="gbardwel" version="1"}
META:FILEATTACHMENT{name="rocrcustomized.png"
attachment="rocrcustomized.png" attr="h" comment="" date="1386966764"
path="rocrcustomized.png" size="47175" user="gbardwel" version="1"}
META:FILEATTACHMENT{name="presentationdetail.png"
attachment="presentationdetail.png" attr="h" comment=""
date="1386966811" path="presentationdetail.png" size="73496"
user="gbardwel" version="1"} META:FILEATTACHMENT{name="presentation.png"
attachment="presentation.png" attr="h" comment="" date="1386967238"
path="presentation.png" size="24283" user="gbardwel" version="1"}
META:FILEATTACHMENT{name="earchitecture.png"
attachment="earchitecture.png" attr="h" comment="" date="1386968613"
path="earchitecture.png" size="4087" user="gbardwel" version="1"}
META:FILEATTACHMENT{name="er.png" attachment="er.png" attr="h"
comment="" date="1386969366" path="er.png" size="35086" user="gbardwel"
version="1"}
