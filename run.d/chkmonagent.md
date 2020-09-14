### Script

The **chkmonagent** script checks the health of the Openview (OMI) agent and cycles the agent if an error is noted.


### Agent Health

<pre># /opt/OV/bin/opcagt -status
midaemon    Measurement Interface daemon                     (18623)  Running
ttd         ARM registration daemon                                   Stopped
perfalarm   Alarm generator                                           Stopped
perfd       real time server                                          Stopped
hpsensor    HP Compute Sensor                   AGENT,OA     (18619)  Running
oacore      Operations Agent Core               AGENT,OA     (18467)  Running
opcacta     OVO Action Agent                    AGENT,EA     (18392)  Running
opcle       OVO Logfile Encapsulator            AGENT,EA     (18405)  Running
opcmona     OVO Monitor Agent                   AGENT,EA     (18660)  Running
opcmsga     OVO Message Agent                   AGENT,EA     (18517)  Running
opcmsgi     OVO Message Interceptor             AGENT,EA     (18674)  Running
ovbbccb     OV Communication Broker             CORE                  Starting
ovcd        OV Control                          CORE         (16203)  Running
ovconfd     OV Config and Deploy                COREXT       (16410)  Running
Agent Health Status: Critical, Time:Fri Apr 13 10:19:14 2018

Message Agent is not buffering.</pre>

As noted in this example, the agent is not healthy. It's noted as in a **Critical** state. The **chkmonagent** script scans the output, ignores the status of **ttd**, **perfalarm**, **perfd** per the Monitoring team recommendations (the modules aren't currently in use) and checks the output for **Isn't Running**, **Stopped**, and **Aborted**. It also checks for the **Agent Health Status**.

If any of these errors are found in the output, the agent is killed and then restarted. An error is logged in the /opt/intrado/var/openview.failed file.


#### Options

You can manage the Openview agent by passing one of three options to the script:

* **kill** - This option creates a flag file called **/opt/intrado/var/openview.kill**. The script will see it on the next run and will kill the agent regardless of whether there's an error in the output. The script will start the agent as normal.
* **stop** - This option creates both the **/opt/intrado/var/openview.kill** flag file which tells the script to kill the agent, and then the **/opt/intrado/var/openview.stop** flag file. The **openview.stop** flag file causes the script to exit without checking or starting the agent.
* **start** - This option removes the **openview.stop** file which then lets the script evaluate the agent if running and start it if not running.

You can also manually put the flag files in the listed locations to force behavior such as disabling or enabling a set of servers in a project.


### Reports

The **/opt/intrado/var/openview.failed** file is retrieved from every server and a report generated in https://incojs01.scc911.com/reports/ovfailed.output

