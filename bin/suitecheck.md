Description: The suitecheck script runs every 5 minutes and checks the run.d directory for any scripts that need to be run more often than the nightly script run.

* Location: [server]:bin/suitecheck

If you create a **bin/runonce** script, the suitecheck script will run that script and then delete it.

