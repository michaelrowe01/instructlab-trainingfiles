META:TOPICINFO{author="rnaranjo" date="1467843390" format="1.1"
version="1.3"} META:TOPICPARENT{name="DatabaseGrowth"}

# Deleting data in Rational Team Concert DKGRAY Authors: Main.DarcyWiborgWeber [deleting-data-in-rational-team-concert-dkgray-authors-main.darcywiborgweber]

Build basis: Rational Team Concert 4.0.x, 5.0.x, 6.x ENDCOLOR

TOC{title="Page contents"}

This document refers to capabilities available in version 4.0 and newer
of Rational Team Concert. It assumes use of the Rational Team Concert
Eclipse client, although many of the functions referenced here are
available from other clients. The functions described here must be
executed by a user with sufficient administrative privileges. See the
last section [Administration](DataDeletionRTC#Administration), for more
information on creating a role with the necessary privileges.

### Summary

### Change Management (Work Items)

**Work item properties**

Work item properties can be edited.

*Note*: The previous and new values are recorded in the work item
history as shown in Figure 1. If the history must be scrubbed, delete
the work item rather than editing it.

Figure 1

**Work item comments**

To delete a work item comment, right click on it and select Empty
Comment. The comment will be replaced with the string, as shown in
Figure 2. All references to the comment are removed from the work item
history.

Figure 2.

*Note*: The date and name of the person who commented is still shown in
the Discussion area. If the persons name must be scrubbed, delete the
work item rather than editing it.

**Work item attachments**

To delete a work item attachment, right click on the attachment and
select Delete.

Figure 3

Deleting an attachment removes all versions of it from the repository.
Links to all versions of the attachment become broken links, as shown in
Figure 4. (Selecting Remove rather than Delete would keep the attachment
in the repository.)

Figure 4.

*Note*: The name of the person who attached or replaced an attachment
continues to be shown in the work item history after the attachment is
deleted. If the persons name must be scrubbed, delete the work item
rather than editing it.

**Work item deletion** To delete a work item, select Delete from its
context menu.

Figure 5.

Deleting a work item deletes it from the repository. Links to that work
item become broken links. The URL itself contains no user-specified
information, only the work item number.

If you want to preserve most of the contents of the work item before
deleting it, for example, because you need to remove history references,
copy the work item using the Create Work Item Copy option as shown in
Figure 6. This will copy a subset of information to a new work item. The
new work item will need to be manually updated with additional
information you want to preserve, such as links and attachments.

Figure 6

For more information about deleting work items, see the following help
topic. [Deleting Work
Items](http://www-01.ibm.com/support/knowledgecenter/SSCP65_5.0.2/com.ibm.team.workitem.doc/topics/t_deleting_work_items.html)

### Source Control Management

**Source code**

Source files cannot be deleted but the contents of a change can be
deleted, as shown in Figure 7.

This step needs to be completed for all changes layered on top of the
content that is being scrubbed, including every version of the change
that was checked in against this change set.

Deleting the contents of a change as shown here will result in an empty
file. If you want to preserve most of the contents of the source file,
and just delete a specific change, have someone create and deliver a new
change set that removes the change BEFORE deleting the contents of the
change.

For more information on deleting content, see the following article:
[https://jazz.net/library/article/1006](https://jazz.net/library/article/1006/)

Inside the RTC repository, the source changes are stored once, and
referenced by the change set, and, in turn, by the components and
baselines that include the change set. Therefore, clearing source
changes in this manner ensures they are removed in all locations where
they are used. Even though a baseline may still have a pointer to the
change set, the content does not exist and therefore will not appear in
the baseline.

*Note*: If the change set has been delivered to a different repository,
this process must be completed in that repository as well.

Copies of source code can also exist in developer sandboxes (a personal
work area stored on the developers local system). Scrub developer
sandboxes using operating system tools, such as searching for the files
containing the changes to be deleted, or reverting to a backup image
from prior to the scrubbing.

**Change sets** A change set cannot be deleted. However, a change sets
title can be changed, and its source contents can be deleted as
described in the previous section.

*Note*: A change sets title (comment) can be edited only by the change
set author. To scrub the title, have the author edit the change set
comment, or temporarily change the authors password so that the
administrator can login as that user to make the change.

Figure 8.

**Components** A component cannot be deleted. The contents of a
component can be deleted as described in the previous sections, and a
component can be renamed. Right click the component and select Rename.

Figure 9.

It is also possible to restrict read access for component. Create a
different project area with restricted access control, and then move the
component to that restricted project area by changing its owner. Links
to all versions of the attachment become broken links, as shown in
Figure 4.

*Note*: External tools that reference a component URL (for example,
using the ClearCase RTC bridge) will still link to it unless changed
externally; however, users without read access will not be able to see
it if they try to open the link.

**Streams** A stream can be renamed or deleted. Components can be
removed from a stream.

**Baselines** A baseline cannot be deleted, however, it can be renamed,
and the contents of a baseline can be deleted as described in the
previous sections, by deleting source changes.

As mentioned earlier, inside the RTC repository, the source changes are
stored once, and referenced by the change set, and, in turn, by the
baselines that include the change set. Therefore, clearing the source
changes as described in a previous section ensures they are removed in
all locations where they are used. Even though a baseline may still have
a pointer to the change set, the source content does not exist and
therefore will not appear in the baseline.

### Administration

Administrative users will need full permissions to edit and delete data
from RTC.

Figure 10.

In the process template, you may want to define a new role such as
Administrator that has full permissions, and assign it to those users
who will participate in data scrubbing. For more information about
setting permissions, see this help topic:
\[\[<http://www-01.ibm.com/support/knowledgecenter/SSCP65_5.0.2/com.ibm.jazz.platform.doc/topics/t_mod_permissions.html>\]\[Modify
Permissions\]

##### Related topics: [Deployment web home](DeploymentWebHome), [Deployment web home](DeploymentWebHome) [related-topics-deployment-web-home-deployment-web-home]

##### Additional contributors: Main.RosaNaranjo [additional-contributors-main.rosanaranjo]

META:FILEATTACHMENT{name="Figure1.png" attachment="Figure1.png" attr=""
comment="" date="1437513850" path="Figure1.png" size="13763"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure2.png"
attachment="Figure2.png" attr="" comment="" date="1437513880"
path="Figure2.png" size="35143" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Figure4.png" attachment="Figure4.png" attr=""
comment="" date="1437513910" path="Figure4.png" size="32042"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure3.png"
attachment="Figure3.png" attr="" comment="" date="1437513948"
path="Figure3.png" size="22338" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Figure5.png" attachment="Figure5.png" attr=""
comment="" date="1437513993" path="Figure5.png" size="79650"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure7.png"
attachment="Figure7.png" attr="" comment="" date="1437514116"
path="Figure7.png" size="24638" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Figure10.png" attachment="Figure10.png"
attr="" comment="" date="1437514525" path="Figure10.png" size="74191"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure6.png"
attachment="Figure6.png" attr="" comment="" date="1437514578"
path="Figure6.png" size="58841" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Figure9.png" attachment="Figure9.png" attr=""
comment="" date="1437514795" path="Figure9.png" size="21408"
user="rnaranjo" version="1"} META:FILEATTACHMENT{name="Figure8.png"
attachment="Figure8.png" attr="" comment="" date="1437514834"
path="Figure8.png" size="22296" user="rnaranjo" version="1"}
META:FILEATTACHMENT{name="Summary.png" attachment="Summary.png" attr=""
comment="" date="1437577948" path="Summary.png" size="116368"
user="rnaranjo" version="1"}
