Description: This script should be configured to run regularly. I generally run it every 5 minutes, YMMV.

1. The script creates, if missing, the defined DATA, LOGS, and RUND directories.

2. The script runs any script located in the RUND/always directory.

2a. If the **runonce** script exists, it will execute and then will be removed.

3. The script will run any script in the RUND/[HHMM] directory during that time.

* Location: [server]:bin/suitecheck

For scripts in the RUND directory structure, you can copy or link any script in the BIN directory into an 
appropriate HHMM directory or the always directory if that's your choice.

If any scripts have a recommended order, a script that needs to run before another script, you can set the 
linked file name to prepend a number or other method for ensuring one script runs before another. Currently 
I'm using the numeric value, 00-99 for such scripts.

