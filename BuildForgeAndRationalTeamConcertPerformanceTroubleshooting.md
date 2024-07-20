# Why does the Rational Team Concert client take a long time to connect to the build agent server?

Authors: IntegrationsTroubleshootingTeam Build basis: Rational
Team Concert 4.x and later 


When running BuildLoopTask or "Test Connection" from a Rational Team
Concert (RTC) client to connect to the build agents server, the process
to get connected to the build server is slow.

## Initial assessment

### Symptoms

-   When you click **Test Connection** under defined build engine in the
    RTC Eclipse client, it takes 10 seconds or more for the results to
    come as a pass.

### Impact/scope

-   This can also contribute to build requests staying in a pending
    state for longer.

## Data gathering and subsequent analysis steps

-   A third party tool can be used to debug this problem
    ([Wireshark](http://www.wireshark.org/))
-   Run Wireshark on the build agent machine and the RTC server machine
    and capture the interfaces that are being used by both machines.
-   Run the "Test Connection" from the RTC client.
-   Now the network communication between the RTC server and the build
    agent machine will be captured in Wireshark along with other network
    communication happening on those machines.
-   Look for the TCP communication that is done from the RTC server
    machine to the build server machine.
-   Use Wireshark filter \*ip.dst == \* on the capture of the build
    machine to filter out unnecessary traces
-   Follow the TCP stream of the RTC server and build machine in
    Wireshark.
-   Check all the communication ASCII output.
-   Look for any other errors reported while checking the source and
    destination IP address in Wireshark.

## Possible causes

-   Following the TCP stream using Wireshark might show the cause of the
    delay in some cases. The long delay to pass the connection test
    might be caused by map drives on the build agent machines that were
    not resolved. Example:

200 HELLO - BuildForge Agent v7.1.2.2-0-0010 cmd ping

username buildadmin

password buildadmin

go

320 AUTH AuthRunningAs\["SYSTEM","NT AUTHORITY",\*WinSidUser\] 320 AUTH
AuthPriv\["..........................."\] 320 AUTH
AuthPriv\[".................."\] 320 AUTH
AuthPriv\["......................................."\] 320 AUTH
AuthPriv\[".................."\] 320 AUTH
AuthPriv\["....................."\] 320 AUTH
AuthPriv\["........................"\] 320 AUTH
AuthPriv\["..........................."\] 320 AUTH
AuthPriv\["....................."\] 320 AUTH
AuthPriv\["........................"\] 320 AUTH
AuthPriv\["............"\] 320 AUTH AuthPriv\[".................."\] 320
AUTH AuthPriv\["..........................."\] 320 AUTH
AuthPriv\["....................."\] 320 AUTH
AuthPriv\[".................."\] 320 AUTH
AuthPriv\["....................."\] 320 AUTH
AuthPriv\["....................."\] 320 AUTH AuthPriv\["............"\]
320 AUTH AuthPriv\["................................."\] 320 AUTH
AuthPriv\[".................."\] 320 AUTH
AuthPriv\[".................."\] 320 AUTH
AuthPriv\[".............................."\] 320 AUTH
AuthPriv\["....................."\] 320 AUTH
AuthPriv\[".............................."\] 320 MAP
MapError\[+53,"\\machine.a\d\$","W:"\] 320 MAP
MapError\[+67,"\\machine.b\DD1 (E)","X:"\] 320 MAP
MapOk\["Y:","\\machine.c\d\$","Microsoft Windows Network"\] 320 MAP
MapError\[+53,"\\machine.e\d\$","Z:"\] 320 AUTH AuthOk\["buildadmin"\]
320 SET EnvSet\["BF_AGENT_VERSION","7.1.2.2-0-0010"\] 320 SET
EnvSet\["BF_AGENT_PLATFORM","Windows 2003"\] 320 EXEC
Locale\["Chinese_Taiwan.950"\] 320 EXEC Locale\["Chinese_Taiwan.950"\]
300 HEARTBEAT 1 310 PLAT Windows 2003 320 PING PingOk 251 RESULT 0 260
EOR quit

## Possible solutions

-   You can see that there are MapErrors reported

320 MAP MapError\[+53,"\\machine.a\d\$","W:"\] 320 MAP
MapError\[+67,"\\machine.b\DD1 (E)","X:"\] 320 MAP
MapOk\["Y:","\\machine.c\d\$","Microsoft Windows Network"\] 320 MAP
MapError\[+53,"\\machine.e\d\$","Z:"\]

-   Remove the mapped network drives that are not getting resolved or
    fix the mapped drives in question so they are accessible.

##### Related topics: 

-   Still need help troubleshooting your integrations issue? Refer to
    [Integrations troubleshooting](IntegrationsTroubleshooting) for
    additional topics.

##### External links: 

-   Wireshark: <http://www.wireshark.org/>

##### Additional contributors: 
-   Main.ZeeshanChoudhry [additional-contributors-main.zeeshanchoudhry]
