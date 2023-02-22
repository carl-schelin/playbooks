Description: This is a [server] script. It's intended to be run on the [server] server. [server] is the hostname of the server.

* This script is installed in bin/[server]

The unixsuite script will run a [server] script if when the unixsuite script runs, it's on the [server] server. This lets you create a script that's intended to run on just the server identified as [server].

The script can do anything specifically for targeted server.


Specific Information:

The status script validates the nagios configuration and validates the integrity of the mysql database files. Errors are reported if found.

