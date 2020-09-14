Description: The chkov script runs every 5 minutes and checks the run.d directory for any scripts that need to be run more often than the nightly script run.

* Location: [server]:/opt/intrado/bin/chkov

The script originally checked the status of the Openview agent and restarted it if in error but that function has been moved to the chkmonagent script. 

If you create a **/opt/intrado/bin/runonce** script, the chkov script will run that script and then delete it.

