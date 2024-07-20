META:TOPICINFO{author="sbeard" date="1385163643" format="1.1"
reprev="1.31" version="1.31"} META:TOPICPARENT{name="WebHome"}

# Deployment wiki formatting guidance [deployment-wiki-formatting-guidance]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

TOC{title="Page contents"}

The Deployment wiki must have a consistent look and feel across all its
sections, subsections, and topics. Always use the standard topic
formatting, particularly for the headers, footers, heading styles, and
fonts. Some of the formatting relates to specific information that is
required on all topic pages.

These guidelines focus on how to create wiki pages and how to complete
and format the different sections of wiki pages. For writing guidelines
about style issues that relate to clarity and consistency within a wiki
page, such as capitalization and spelling, see [Deployment wiki writing
guidelines](DeploymentWritingGuidelines).

## Deployment wiki topic page template

All new topic pages in the Deployment wiki are created by using the
WebTopicEditTemplate. All pages must adhere to this template to maintain
the overall look and feel of the wiki.

DO:

-   When you create a topic page, change the placeholder title: ---+!
    Topic title (use a lowercase style, which is known as
    "sentence-style" capitalization)

<!-- -->

-   When you create a topic page, set the initial authors: DKGRAY
    Authors: Main.TWikiUser, Main.TWikiUser The list of authors should
    be a comma-separated list, where each author is represented by their
    TWiki name Main.TwikiUser; for example: Main.StevenBeard RED
    **Note:** ENDCOLOR The name that is displayed in the upper-right and
    the history of the page is not necessarily a person who made
    significant contributions to a topic page. A key aim of the wiki is
    to ensure that authors and additional contributors are recognized
    for their contribution, both internally to their organization and in
    the wider community. The authors who are listed in the title banner
    for a topic page should be the people who have made major
    contributions to developing the page, regardless of who edited the
    wiki page. The number of authors should be kept to a reasonable
    number (4- 10 maximum). If an entire section or sub-section team was
    instrumental in developing a page, use a link to the respective
    section or sub-section; for example: [Deployment planning and design
    team](DeploymentPlanningAndDesign)

<!-- -->

-   When you create a topic page, set the build basis: Build Basis:
    Products, Editions and Versions as applicable The build basis should
    either reflect the most specific build basis that is appropriate for
    the page or be explicitly set to "None."

<!-- -->

-   All topic pages must have an initial introduction paragraph or two
    before the first heading.

<!-- -->

-   All topic pages must have a list of related topics, external links,
    and additional contributors at the bottom of the page, in accordance
    with the template format.

DO NOT:

-   Do not edit or remove the page contents or margin:

TOC{title="Page contents"}

-   Do not alter the default heading styles and fonts or paragraph
    fonts.

<!-- -->

-   Do not remove the final line of markup:

\#StatusIcons

## Topic page status icons

Use these status icons for all topic pages to indicate the page status:

-    **To do:** Indicates a new topic page that has not been started. By
    default, all pages created from the [topic page
    template](WebTopicEditTemplate) will include this icon.

<!-- -->

-    **Under construction:** Indicates that a topic page is being edited
    or reviewed.

<!-- -->

-    **New:** Indicates that a topic page was recently created and
    reviewed. Use this icon only for significant new content within the
    wiki and not for external links. Typically, new icons will be
    removed after 1-2 months.

<!-- -->

-    **Updated:** Indicates that a topic page was recently updated and
    reviewed. This icon can also be used to indicate external content
    that has been migrated into the wiki, such as Jazz.net articles.
    **Use this status icon for Jazz.net articles or other already
    externally available content when it is initially migrated into the
    wiki.** Typically, updated icons will be removed after 1-2 months.

\* **Constant change:** Indicates that a topic page is constantly under
change by the wider wiki community.

-   **None:** If a status icon is not displayed, the topic page is
    deemed to be in a stable unchanging state.

Add icons before the title in the title box of a topic page:

# Title of the topic page [title-of-the-topic-page]

DKGRAY Authors: Main.StevenBeard Build basis: None ENDCOLOR

RED **Note:** ENDCOLOR All topic pages that only technical leaders and
senior editors (aka Main.TWikiDeploymentAuthorsGroup) can edit must use
the above status icon conventions. All topic pages that deployment
practitioners (aka Main.TWikiAuthorsGroup and
Main.TWikiExternalAuthorsGroup) can edit must use the above status icon
convention where possible. Typically, open community pages will use the
constant change icon to denote that they might be under constant change.

Smaller versions of the status icons \[ ) can be used in front of
navigation links, such as on section pages, to indicate the status of
the linked topic page. **Note: Avoid using the smaller constant change
icon in front of navigation links.** It is important that this icon and
the one on the topic page are the same; for example:

-    [Deployment planning: Where to start? ](DeploymentPlanning)

## Personal user profile pages

You can create a personal user profile page that will be linked to from
your Main.TWikiUsers name; for example: Main.StevenBeard. Copy the
formatting and layout of this example.

## General formatting guidelines

### Making a comment or a note

To make a comment or to mark something you want to return to, use three
number signs: \###. The number signs do not affect the formatting and
are easy to spot.

### Adding a questions and comment box to a topic

You can add a questions and comments box to a page that has restrictive
write access to allow additional TWikiGroups or all Jazz.net users to
ask a question or comment. The following example is the best mechanism
for adding a questions and comments box that has a writable subtopic to
collect the comments. To view the markup of the example, view this topic
in Raw View.

##### Questions and comments: [questions-and-comments]

COMMENT{type="below" target="DeploymentFormattingGuidanceComments"
button="Submit"}

INCLUDE{"DeploymentFormattingGuidanceComments"}

RED **Note:** ENDCOLOR On the subtopic questions and comments page, you
must explicitly set the write access to the correct level. To allow
everyone to comment or raise a question, set ALLOWTOPICCHANGE to a blank
list:

To see the correct format and layout, view the
DeploymentFormattingGuidanceComments subtopic in Raw View.

RED **Note:** ENDCOLOR In most cases, put the questions and comment box
at the bottom of a topic page, below the list of additional authors.

## TWiki editing shorthand

RED **Note:** ENDCOLOR Use **Edit** instead of the WYSIWYG edit because
the WYSIWYG editor does not work correctly in all browsers.

STARTINCLUDE

Formatting Command

What you type

What you get

\#TheParagraphs **Paragraphs:** BR Blank lines create paragraphs.

1st paragraph

2nd paragraph

1st paragraph

2nd paragraph

\#TheHeadings **Headings:** BR Three or more hyphens (-) at the
beginning of a line, followed by plus signs (+) and the heading text.
One plus sign creates a top level heading; two plus signs create a
second level heading, etc. The maximum heading depth is 6.

T You can create a table of contents with the [TOC](VarTOC) variable. BR
T To exclude a heading from the TOC, put `!!` after the `---+`. BR X
Empty headings are allowed and are not displayed in the table of
contents.

## Sushi

### Maguro

### Not in TOC [not-in-toc]

Sushi Maguro Not in TOC

\#BoldText **Bold Text:** BR To make a word **bold**, enclose it in
asterisks (`*`).

**Bold**

**Bold**

\#ItalicText **Italic Text:** BR To make a word *italic*, enclose it in
underscores (`_`).

*Italic*

*Italic*

\#BoldItalic **Bold Italic:** BR To make a word ***bold italic***,
enclose it in double-underscores (`__`).

***Bold italic***

***Bold italic***

\#FixedFont **Fixed Font:** BR To make a word `fixed font`, enclose it
in equal signs (`=`).

`Fixed font`

`Fixed font`

\#BoldFixedFont **Bold Fixed Font:** BR To make a word
**`bold fixed font`**, enclose it in double equal signs (`==`).

**`Bold fixed`**

**`Bold fixed`**

T You can follow the closing bold, italic, or other (=\* \_ \_\_ = `=`)
indicator with normal punctuation, such as commas and full stops. BRX
Make sure that no spaces are between the text and the indicators. BRX
All words that are enclosed by the indicators must be on the same line.

*This works*, \_this does not \_ *this fails too*

*This works*, BR \_this does not \_ BR *this fails too*

\#HorizontalRule **Separator (Horizontal Rule):** BR Place three or more
hyphens at the beginning of a line.

-------

-------

\#BulletedList **Bulleted List:** BR Type a multiple of three spaces, an
asterisk, and another space. BRH For all list types, you can break a
list item over several lines by indenting lines after the first one by
at least 3 spaces.

-   level 1
    -   level 2
-   back on 1
-   A bullet broken over three lines
-   last bullet

<!-- -->

-   level 1
    -   level 2
-   back on 1
-   A bullet broken over three lines
-   last bullet

\#IconList **Icon List:** BR Type a multiple of three spaces, an
asterisk, text `icon:name` and another space. BRH Use the `name` of any
[TWikiDocGraphics](http://twiki.org/cgi-bin/view/TWiki/TWikiDocGraphics)
icon.

-   ICON{tip} Icon list
    -   ICON{led-red} Full
    -   ICON{led-green} OK
-   ICON{unchecked} Item 1
-   ICON{checked} Item 2
-   ICON{empty} No bullet

<!-- -->

-   ICON{tip} Icon list
    -   ICON{led-red} Full
    -   ICON{led-green} OK
-   ICON{unchecked} Item 1
-   ICON{checked} Item 2
-   ICON{empty} No bullet

\#NumberedList **Numbered List:** BR Type a multiple of three spaces, a
list type character, a period, and another space. Several list types are
available besides a number:

| Type | Generated Style          | Sample Sequence   |
|:-----|:-------------------------|:------------------|
| 1\.  | Arabic numerals          | 1, 2, 3, 4...     |
| A.   | Uppercase letters        | A, B, C, D...     |
| a\.  | Lowercase letters        | a, b, c, d...     |
| I.   | Uppercase Roman Numerals | I, II, III, IV... |
| i\.  | Lowercase Roman Numerals | i, ii, iii, iv... |

1.  Sushi
2.  Dim Sum
3.  Fondue

<!-- -->

1.  Sushi
2.  Dim Sum
3.  Fondue

<!-- -->

1.  Sushi
2.  Dim Sum
3.  Fondue

<!-- -->

1.  Sushi
2.  Dim Sum
3.  Fondue

<!-- -->

1.  Sushi
2.  Dim Sum
3.  Fondue

<!-- -->

1.  Sushi
2.  Dim Sum
3.  Fondue

\#DefinitionList **Definition List:** BR Type three spaces, a dollar
sign, the term, a colon, and a space, followed by the definition.

Deprecated syntax: Type three spaces, the term with no spaces, a colon,
and a space, followed by the definition.

Sushi
:   Japan

Dim Sum
:   S.F.

<!-- -->

Sushi
:   Japan

Dim Sum
:   S.F.

\#TheTable **Table:** BR Each row of the table is a line containing of
one or more cells. Each cell starts and ends with a vertical bar (\|).
Any spaces at the beginning of a line are ignored.

-   `| *bold* |` header cell with text in asterisks
-   `|   center-aligned   |` cell with at least two, and an equal number
    of spaces on either side
-   `|      right-aligned |` cell with more spaces on the left
-   `| 2 colspan ||` and multi-span columns with multiple \|'s right
    next to each other
-   `|^|` cell with caret indicating follow-up row of multi-span rows
-   You can split rows over multiple lines by putting a backslash (`\`)
    at the end of each line
-   Contents of table cells wrap automatically as determined by the
    browser
-   To add `|` characters in tables, use `VBAR` or `|` .
-   To add `^` characters in tables, use `CARET` or `^` .

T The SYSTEMWEB.TablePlugin provides the `|^|` multiple-span row
functionality and additional rendering features

| L          | C     | R       |
|:-----------|:------|:--------|
| A2         | B2    | C2      |
| A3         | B3    | C3      |
| multi span |       |         |
| A5-7       | 5     | 5       |
| \^         | six   | six     |
| \^         | seven | seven   |
| split      | over  | 3 lines |
| A9         | B9    | C9      |

| L          | C     | R       |
|:-----------|:------|:--------|
| A2         | B2    | C2      |
| A3         | B3    | C3      |
| multi span |       |         |
| A5-7       | 5     | 5       |
| \^         | six   | six     |
| \^         | seven | seven   |
| split      | over  | 3 lines |
| A9         | B9    | C9      |

\#WikiWordLinks **WikiWord Links:** BR CapitalizedWordsStuckTogether (or
WikiWords) produce a link automatically if they are preceded by a space
or parenthesis. BRT To link to a topic in a different web, type
`Otherweb.TopicName`. BRT To link to a topic in a subweb, type
`Otherweb.Subweb.TopicName`. BRH The link label excludes the name of the
web; for example, only the topic name is shown. As an exception, the
name of the web is shown for the HOMETOPIC topic. BRX Dots `'.'` are
used to separate webs and subwebs from topic names and cannot be used in
topic names.

Use the TWikiVariables SYSTEMWEB and USERSWEB instead of TWiki and Main.

WebStatistics

Sandbox.WebNotify

Sandbox.WebHome

Sandbox.Subweb.TopicName

WebStatistics

Sandbox.WebNotify

Sandbox.HOMETOPIC

TopicName

\#TheAnchors **Anchors:** BR You can define a reference inside a TWiki
topic (called an anchor name) and link to that. To define an anchor,
type `#AnchorName` at the beginning of a line. The anchor name must be a
WikiWord of no more than 32 characters. To link to an anchor name, use
the `[[MyTopic#MyAnchor]]` syntax. If you want to link within the same
topic, you can comit the topic name

[WikiWord#NotThere](WikiWord#NotThere)

[Jump](#MyAnchor)

\#MyAnchor To here

[WikiWord#NotThere](WikiWord#NotThere)

[Jump](#MyAnchor)

\#MyAnchor To here

\#ExternalLinks **External Links:** BR URLs that start with `file`,
`ftp`, `gopher`, `http`, `https`, `irc`, `mailto`, `news`, `nntp` and
`telnet` are linked automatically if they are preceded by a space or
parenthesis. External links are indicated by a trailing
ICON{external-link} icon, and open in a new browser tab or window. Link
behavior can be set in configure. To prevent links, add an exclamation
point (`!`) as a prefix.

<http://twiki.org>

<https://google.com>

http://escaped-link

<http://twiki.org>

<https://google.com>

http://escaped-link

\#ForcedLinks \#HeRe **Forced Links:** BR Use double square brackets to
create forced links: To force a link, type `[[link]]` or
`[[link][label]]`. Use the former example for singleton words and if
[automatic linking is disabled](#DisableLinks). Use the latter example
to specify a link label other than the link. For the link, you can use
internal link references, such as WikiWords, and URLs; for example:
http://TWiki.org/. BRT Anchor names can be added to create a link to a
specific place in a document. BRT To "escape" double square brackets
that would otherwise make a link, add an exclamation point as a prefix
of the leading left square bracket. BRT If the SHOWTOPICTITLELINK
preferences setting is enabled, the [topic title](VarTOPICTITLE) instead
of the topic name is shown for `[[WikiWord]]` links.

[WikiWord](WikiWord)

[WikiWord#TheSyntax](WikiWord#TheSyntax)

[wiki syntax](WikiSyntax)

[GNU](http://gnu.org/)

[Singleton](Singleton)

escaped: \[\[WikiSyntax\]\]

[WikiWord](WikiWord)

[WikiWord#TheSyntax](WikiWord#TheSyntax)

[wiki syntax](WikiSyntax)

[GNU](http://gnu.org/)

[Singleton](Singleton)

escaped: \[\[WikiSyntax\]\]

\#TopicTitleLinks **Topic Title Links:** BR Use double square brackets
and a plus sign to create links with topic title: To show the [topic
title](VarTOPICTITLE) instead of the topic name, type `[[+TopicName]]`
or `[[+Web.TopicName]]`. The topic title is defined by the form field
named "Title", the topic preferences setting named TITLE, or the topic
name if neither exists. BRT An alternative syntax is
`[[TopicName][$topictitle]]` or `[[Web.TopicName][$topictitle]]`.

[+BugN1234](+BugN1234)

[+Bugs.BugN1234](+Bugs.BugN1234)

[\$topictitle](BugN1234)

[The sky is falling](TOPIC)

[The sky is falling](TOPIC)

[The sky is falling](TOPIC)

\#PreventLink **Prevent a Link:** BR Prevent a WikiWord from being
linked by prepending it with an exclamation point.

SunOS

SunOS

\#DisableLinks **Disable Links:** BR You can disable automatic linking
of WikiWords by surrounding text with == and == tags. BRH To turn off
all auto-linking, use the NOAUTOLINK preferences setting.

RedHat & SuSE

RedHat & SuSE

\#MailtoLinks **Mailto Links:** BR E-mail addresses are linked
automatically. To create e-mail links that have more descriptive link
text, specify subject lines or message bodies, or omit the e-mail
address, you can write `[[mailto:user@domain][descriptive text]]`.

<a@b.com>

\[\[mailto:<a@b.com>\]\\ \[Mail\]\]

[Hi](mailto:?subject=\
Hi)

<a@b.com>

\[\[mailto:<a@b.com>\]\\ \[Mail\]\]

[Hi](mailto:?subject=Hi)

\#TwitterLinks **Twitter Links:** BR @twitter IDs are linked
automatically. The link rule is defined by the
`{Links}{TwitterUrlPattern}` configure setting.

@twiki

@twiki

\#VerbatimText **Verbatim Text:** BR Surround code excerpts and other
formatted text with == and == tags. BRT The `verbatim` tag disables HTML
code. If you want the HTML code within the tags to be interpreted, use
== and == tags instead. BRX Preferences variables (\* Set NAME = value)
are set within verbatim tags.

class CatAnimal { void purr() {

} }

class CatAnimal { void purr() {

} }

\#LiteralText **Literal Text:** BR TWiki generates HTML code from TWiki
shorthand. Experts can surround anything that must be output literally
in the HTML code, without the application of TWiki shorthand rules, with
`..` tags. BRX Any HTML within literal tags must be well formed; that
is, all tags must be properly closed before the end of the literal
block. BRI TWiki Variables are expanded within literal blocks.

|     |     |       |
|-----|-----|-------|
| Not | A   | Table |

|     |     |       |
|-----|-----|-------|
| Not | A   | Table |

\#ProtectedText **Protected Text:** BR Experts can protect text from
mangling by WYSIWYG editors by using `..` tags. Sticky tags do not
affect normal topic display; they are relevant only when content must be
protected from a WYSIWYG editor (usually because content is not
well-formed HTML, or because it is HTML that a WYSIWYG editor might
filter out or modify). Protected content is displayed as plain text in
the WYSIWYG editor.

This div is required

This div is required

STOPINCLUDE

##### Related topics: \* [Deployment wiki writing guidelines](DeploymentWritingGuidelines) [related-topics-deployment-wiki-writing-guidelines]

-   [Example topic: Standard Collaborative Lifecycle Management
    topologies](ExampleTopicStandardCLMTopologies)

##### External links: \* None [external-links-none]

##### Additional contributors: None [additional-contributors-none]
