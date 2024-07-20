META:TOPICINFO{author="websmith" date="1483646377" format="1.1"
reprev="1.6" version="1.6"}

# CLM Version 6.0.1 OSLC API Changes for Enumerations DKGRAY Authors: Main.LarrySmith [clm-version-6.0.1-oslc-api-changes-for-enumerations-dkgray-authors-main.larrysmith]

Build basis: Products, editions, or versions that apply to the content.
If no build basis applies to this content, set the build basis to None.
ENDCOLOR

TOC{title="Page contents"}

This document describes some changes made to the OSLC V2.0 API in RTC
Version 6.0.1. The changes were made to enable specific reports that
required the API to be more compliant with the standard.

There are two OSLC REST API changes made in 6.0.1 that could potentially
break scripts that use the OSLC REST API from prior versions. These
changes are considered improvements over previous releases and were
necessary for standards compliance and to enable cross-project reporting
to work in Report Builder.

-   The first item changes the way enumerations literal URI's are
    specified in responses.
-   The second item changes the response to a JSON request for an
    enumeration so it is a JSON object instead of array of literals.

## The Resource URI of an Enumeration Literal Changes in RTC Version 6.0.1

RTC allows user to specify External Value of enumeration literal. The
literal is configured in the project area administration as follows:

The way this literal is returned in an OSLC response has changed in RTC
Version 6.0.1

### Before RTC Version 6.0.1: Enumeration without an External Value

**Before RTC Version 6.0.1**, consider an enumeration literal without an
external value:

Before RTC Version 6.0.1, if user doesnt specify an External Value and
then does an OSLC GET on the enumeration literal resource, the literal
is referenced with the internal value:

For example, a GET request:

would return a response:

Low priority.literal.1

This does not change in RTC Version 6.0.1 because there is no external
value.

### Before RTC Version 6.0.1: Enumeration with an External Value

**Before RTC Version 6.0.1**, consider an enumeration literal with an
external value:

Before RTC Version 6.0.1, if user does specify an external value and
then does an OSLC GET on the enumeration literal resource, the literal
is referenced with the external value:

Notice how the literal value is used in the reference URI.

For example, a GET request:

would return a response:

Low priority.literal.1

When the external value changes, these URI's will note be valid anymore.

## After RTC Version 6.0.1 the URI is Stable

One drawback of the initial implementation is that the enumeration
literal resource URI is not stable. The URI can change if the user
changes the enumeration value of the enumeration literal. Since the
enumeration literal URI is embedded in every work item and enumeration
resources referenced, the links and data becomes invalid when the
enumeration value changes.

In 6.0.1 release, the URI is made more stable by always using the
internal literal value in the reference and adding an *owl:sameAs*
triple in the resource to map the value properly. The value of
owl:sameAs triple is the external URI of the enumeration literal.

For more information see Best Practice: Use URIs to Represent Enumerated
Values.

### After RTC Version 6.0.1: Enumeration with External Value

In RTC Version 6.0.1 and later, consider if user does specify external
value for the literal:

Now when an OSLC GET is requested for the enumeration literal resource,
the literal is referenced with the internal value and an *owl:sameAs*
element is added:

...

...

Notice how the literal value is not used in the reference URI and is
mapped by the *owl:sameAs* element. Now the administrator is free to
change the literal value without invalidating the links. Because the
*owl:sameAs* resolves the links correctly, the pre-6.0.1 user scenarios
is still supported as the literal resource can be accessed using either
URI.

For example, a GET request:

would return a response:

Low priority.literal.1

The new URI format is more stable for some configurations.

## Enumeration Requests Return a JSON Object instead of an Array

Before RTC Version 6.0.1, when user gets an application/json
representation of an enumeration resource, the returned resource was
returned as a JSON array of enumeration literals. However, array
returned for the enumeration resource does not contain any information
about the enumeration itself. It only lists the enumeration literals. In
6.0.1, a JSON object is returned instead, and this includes information
about enumeration itself in the resource representation.

### Before RTC Version 6.0.1: Enumeration JSON Response

For example, **before RTC Version 6.0.1**, a GET request:

would return an array as a response.

\[ { "rdf:type":\[ {
"rdf:resource":"[http:\\\\jazz.net\\xmlns\\prod\\jazz\\rtc\\cm\\1.0\\Literal](http:\/\/jazz.net\/xmlns\/prod\/jazz\/rtc\/cm\/1.0\/Literal)"
} \],
"rtc_cm:iconUrl":"[https:\\\\localhost:9443\\ccm\\service\\com.ibm.team.workitem.common.internal.model.IImageContentSe](https:\/\/localhost:9443\/ccm\/service\/com.ibm.team.workitem.common.internal.model.IImageContentSe)
rvice\\processattachment\\\_gxHFEC51EeauNJ_abwY7Dg\\enumeration\\low.gif",
"dcterms:title":"Low",
"rdf:about":"[https:\\\\localhost:9443\\ccm\\oslc\\enumerations\\\_gxHFEC51EeauNJ_abwY7Dg\\priority\\priority.literal.1](https:\/\/localhost:9443\/ccm\/oslc\/enumerations\/_gxHFEC51EeauNJ_abwY7Dg\/priority\/priority.literal.1)",
"dcterms:identifier":"priority.literal.1" },

{ "rdf:type":\[ {
"rdf:resource":"[http:\\\\jazz.net\\xmlns\\prod\\jazz\\rtc\\cm\\1.0\\Literal](http:\/\/jazz.net\/xmlns\/prod\/jazz\/rtc\/cm\/1.0\/Literal)"
} \],
rtc_cm:iconUrl":"[https:\\\\localhost:9443\\ccm\\service\\com.ibm.team.workitem.common.internal.model.IImageContentSe](https:\/\/localhost:9443\/ccm\/service\/com.ibm.team.workitem.common.internal.model.IImageContentSe)
rvice\\processattachment\\\_gxHFEC51EeauNJ_abwY7Dg\\enumeration\\high.gif",
"dcterms:title":"High",
"rdf:about":"[https:\\\\localhost:9443\\ccm\\oslc\\enumerations\\\_gxHFEC51EeauNJ_abwY7Dg\\priority\\priority.literal.2](https:\/\/localhost:9443\/ccm\/oslc\/enumerations\/_gxHFEC51EeauNJ_abwY7Dg\/priority\/priority.literal.2)",
"dcterms:identifier":"priority.literal.2" } \]

The array only provides information about the literals and does not
contain any information about the enumeration.

### After RTC Version 6.0.1: Enumeration JSON Response

**After RTC Version 6.0.1**, the resource is returned as a a JSON
object. For example, in RTC Version 6.0.1, a GET request:

now returns a JSON object as a response:

{ "rdf:type": \[ {
"rdf:resource":"[http:\\\\www.w3.org\\2000\\01\\rdf-schema#Class](http:\/\/www.w3.org\/2000\/01\/rdf-schema#Class)"
} \],
"rdf:about":"[https:\\\\localhost:9443\\jazz\\oslc\\enumerations\\\_gxHFEC51EeauNJ_abwY7Dg\\priority](https:\/\/localhost:9443\/jazz\/oslc\/enumerations\/_gxHFEC51EeauNJ_abwY7Dg\/priority)",
"acc:accessContext": {
"rdf:resource":"[https:\\\\localhost:9443\\jazz\\acclist#\_gxHFEC51EeauNJ_abwY7Dg](https:\/\/localhost:9443\/jazz\/acclist#_gxHFEC51EeauNJ_abwY7Dg)"
}, "prefixes": {
"rtc_cm":"[http:\\\\jazz.net\\xmlns\\prod\\jazz\\rtc\\cm\\1.0\\](http:\/\/jazz.net\/xmlns\/prod\/jazz\/rtc\/cm\/1.0\/)",
"oslc":"http:\\\\open-services.net\\ns\\core#",
"owl":"http:\\\\www.w3.org\\2002\\07\\owl#",
"rdf":"http:\\\\www.w3.org\\1999\\02\\22-rdf-syntax-ns#",
"acc":"http:\\\\open-services.net\\ns\\core\\acc#",
"dcterms":"[http:\\\\purl.org\\dc\\terms\\](http:\/\/purl.org\/dc\/terms\/)"
}, "oslc:results": \[ { "rdf:type": \[ {
"rdf:resource":"[https:\\\\localhost:9443\\jazz\\oslc\\enumerations\\\_gxHFEC51EeauNJ_abwY7Dg\\priority](https:\/\/localhost:9443\/jazz\/oslc\/enumerations\/_gxHFEC51EeauNJ_abwY7Dg\/priority)"
}, {
"rdf:resource":"[http:\\\\jazz.net\\xmlns\\prod\\jazz\\rtc\\cm\\1.0\\Literal](http:\/\/jazz.net\/xmlns\/prod\/jazz\/rtc\/cm\/1.0\/Literal)"
} \],
"rtc_cm:iconUrl":"[https:\\\\localhost:9443\\jazz\\service\\com.ibm.team.workitem.common.internal.model.IImageContentSe](https:\/\/localhost:9443\/jazz\/service\/com.ibm.team.workitem.common.internal.model.IImageContentSe)
rvice\\processattachment\\\_gxHFEC51EeauNJ_abwY7Dg\\enumeration\\low.gif",
"dcterms:title":"Low",
"rdf:about":"[https:\\\\localhost:9443\\jazz\\oslc\\enumerations\\\_gxHFEC51EeauNJ_abwY7Dg\\priority\\priority.literal.1](https:\/\/localhost:9443\/jazz\/oslc\/enumerations\/_gxHFEC51EeauNJ_abwY7Dg\/priority\/priority.literal.1)",
"dcterms:identifier":"priority.literal.1" }, { "rdf:type": \[ {
"rdf:resource":"[https:\\\\localhost:9443\\jazz\\oslc\\enumerations\\\_gxHFEC51EeauNJ_abwY7Dg\\priority](https:\/\/localhost:9443\/jazz\/oslc\/enumerations\/_gxHFEC51EeauNJ_abwY7Dg\/priority)"
}, {
"rdf:resource":"[http:\\\\jazz.net\\xmlns\\prod\\jazz\\rtc\\cm\\1.0\\Literal](http:\/\/jazz.net\/xmlns\/prod\/jazz\/rtc\/cm\/1.0\/Literal)"
} \],
"rtc_cm:iconUrl":"[https:\\\\localhost:9443\\jazz\\service\\com.ibm.team.workitem.common.internal.model.IImageContentSe](https:\/\/localhost:9443\/jazz\/service\/com.ibm.team.workitem.common.internal.model.IImageContentSe)
rvice\\processattachment\\\_gxHFEC51EeauNJ_abwY7Dg\\enumeration\\high.gif",
"dcterms:title":"High",
"rdf:about":"[https:\\\\localhost:9443\\jazz\\oslc\\enumerations\\\_gxHFEC51EeauNJ_abwY7Dg\\priority\\priority.literal.2](https:\/\/localhost:9443\/jazz\/oslc\/enumerations\/_gxHFEC51EeauNJ_abwY7Dg\/priority\/priority.literal.2)",
"dcterms:identifier":"priority.literal.2" } \] }

Here we see more information about the Enumeration available in the
object attributes.

##### External links: [external-links]

Referenced Items:

-   Task 366205: Enumeration owl:sameAs implementation does not work as
    expected\]
-   Task 360439: Enumeration should have rdf:type of rdfs:Class &
    Enumeration Literal should have rdf:type of its owner Enumeration

META:FILEATTACHMENT{name="oslc-fig1-Low.png"
attachment="oslc-fig1-Low.png" attr="h" comment="Configuring an
Enumeration external value" date="1483635562" path="oslc-fig1-Low.png"
size="315509" user="websmith" version="1"}
META:FILEATTACHMENT{name="oslc-fig2-Low.png"
attachment="oslc-fig2-Low.png" attr="h" comment="Enumeration
Configuration of Low without External Value" date="1483635873"
path="oslc-fig2-Low.png" size="64417" user="websmith" version="1"}
META:FILEATTACHMENT{name="oslc-fig3-GET.png"
attachment="oslc-fig3-GET.png" attr="h" comment="OSLC Get Request"
date="1483635899" path="oslc-fig3-GET.png" size="50512" user="websmith"
version="1"} META:FILEATTACHMENT{name="oslc-fig4-GET.png"
attachment="oslc-fig4-GET.png" attr="h" comment="OSLC Get Request"
date="1483635926" path="oslc-fig4-GET.png" size="36048" user="websmith"
version="1"} META:FILEATTACHMENT{name="oslc-fig5a-GET-xml.png"
attachment="oslc-fig5a-GET-xml.png" attr="h" comment="OSLC Get XML"
date="1483636740" path="oslc-fig5a-GET-xml.png" size="35813"
user="websmith" version="1"}
META:FILEATTACHMENT{name="oslc-fig6-GET.png"
attachment="oslc-fig6-GET.png" attr="h" comment="OSLC GET XML"
date="1483636773" path="oslc-fig6-GET.png" size="76333" user="websmith"
version="1"} META:FILEATTACHMENT{name="oslc-fig5-Low.png"
attachment="oslc-fig5-Low.png" attr="h" comment="Enumeration with
external value" date="1483639206" path="oslc-fig5-Low.png" size="66901"
user="websmith" version="1"}
META:FILEATTACHMENT{name="oslc-fig9-GET-json.png"
attachment="oslc-fig9-GET-json.png" attr="h" comment="Get JSON"
date="1483641981" path="oslc-fig9-GET-json.png" size="75793"
user="websmith" version="1"}
META:FILEATTACHMENT{name="oslc-fig10-GET-json.png"
attachment="oslc-fig10-GET-json.png" attr="h" comment="GET JSON"
date="1483641999" path="oslc-fig10-GET-json.png" size="75245"
user="websmith" version="1"}
META:FILEATTACHMENT{name="oslc-fig6a-GET.png"
attachment="oslc-fig6a-GET.png" attr="h" comment="GET rdf by literal"
date="1483642308" path="oslc-fig6a-GET.png" size="33268" user="websmith"
version="1"}
