META:TOPICINFO{author="paulellis" date="1506610908" format="1.1"
version="1.13"} META:TOPICPARENT{name="DeploymentTroubleshooting"}

# How to start a troubleshooting assessment [how-to-start-a-troubleshooting-assessment]

DKGRAY Authors: Main.GrantCovell, Main.DeniseMcKinnon Build basis: None
ENDCOLOR

TOC{title="Page contents"}

Assessing the scope of the situation can help you narrow down a list of
possible causes. Included below are some questions to keep in mind as
you investigate. These questions provide general guidance for getting
started and isolating the source of the problem.

## Symptoms (What?)

-   Can you clearly describe the problem? When you do X, Y happens.
-   What are the actions that cause the problem to occur?
-   What operations were you trying to execute?
-   What error messages are displayed? Can you get to the logs and list
    the errors in there?
-   In which user interfaces does the issue occur? (For example, web
    client versus Eclipse client)

## Impact(Who?)

**Question**: Which users are impacted by this issue?

|  |
|----|
| **Answer**: Bob is the only one who takes a long time to log in to the application. |

-   **Implication**: A problem that occurs for a single user might
    suggest something unique about the user.
-   **Implication**: A problem that occurs for a specific group suggests
    something unique about the group, or a network problem specific to a
    location.
-   **Implication**: A problem that occurs for everyone regardless of
    location suggests an issue at the server location, i.e. network,
    server, or the database.

**Question**: Where are the users located who are seeing this issue?

|  |
|----|
| **Answer**: Queries take a long time to respond for users in Brazil and China. |

-   **Implication**: A problem that occurs for a particular geography
    suggests a network problem.

## Timing(When?)

**Question**: When did the problem first start?

|                                               |
|-----------------------------------------------|
| **Answer**:The problem started last Thursday. |

-   **Implication**:There were some changes made on or before last
    Thursday that might be contributing to the situation.

**Question**: When does the problem re-occur?

|                                                       |
|-------------------------------------------------------|
| **Answer**:The problem seems worse right after lunch. |

-   **Implication**:There are differences in the usage or activities
    performed in the afternoon that are different than the morning. What
    are those differences?

## Environmental changes (Where?)

**Question**: What hardware or software changes have occurred on the
server?

|                                                                      |
|----------------------------------------------------------------------|
| **Answer**: The operating system was upgraded to the latest version. |

-   **Implication**: The changes introduced an incompatibility or
    resulted in an unsupported configuration.
-   **Implication**: The optimisations applied to the previous operating
    system have not been reapplied?
-   **Implication**: The new operating system may require more resources
    to deliver the same performance?

**Question**: How has changed network recently?

|  |
|----|
| **Answer**: A new firewall was installed in the building were the affected users work. |

-   **Implication**: Those changes might have impacted network access or
    introduced authentication issues.

**Question**: What has changed on the computers used by the end users?

|                                                              |
|--------------------------------------------------------------|
| **Answer**: Users who changed browsers are seeing the issue. |

-   **Implication**: The new browser introduced incompatibilities or
    might not be supported.

##### Related topics: None [related-topics-none]

##### External links: [external-links]

-   None

##### Additional contributors: None [additional-contributors-none]
