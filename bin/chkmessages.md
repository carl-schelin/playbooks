==Background==

Message files on servers tend to have a lot of information that's not caught by the monitoring environment. As such, reviewing messages is a good thing as it can identify little things before they become big things.

===Locations===

On servers, the '''chkmessages''' script is located in bin. The '''messages.exclude''' file is located in etc.

'''NOTE''' The local copy of the '''messages.exclude''' file is managed on the source code server in /opt/static/unixsuite/etc. If you need to make changes, make sure the final changes are added to this data file.

On the central server, the '''chkmessages''' script is located in admin/bin. The '''messages.exclude''' file is located in admin/etc.

Currently the script and data file are not source code managed but that will change. The data file will be located on the source code server in /opt/static/admin/etc.

As the central server processes each individual servers log files, the temporary file is located in admin/logs/report as report.YYYYMMDD. Once done, the file is copied to /usr/local/httpd/htsecure/messages

===Process===

# Source code server runs /opt/code/makeunixsuite to build the sync repository. Files are collected from /opt/code/unixsuite and /opt/static/unixsuite and located in /opt/stage/unixsuite.
# Source code syncs /opt/stage/unixsuite with [management server]:admin/install/unixsuite.
# Management server pushes all the bin and etc files to each server.
# Local server runs the '''chkmessages''' script and uses '''messages.exclude''' to parse the log file and write to /var/tmp/messages.
# Unix service account retrieves every server's log file.
# Unix service account runs the '''chkmessages''' script and uses '''messages.exclude''' to parse all the log files and writes to the report log directory.
# When done, the Unix service account copies the final report file to /usr/local/httpd/htsecure/messages

===Permissions===

The various log files can have various different permissions. On Linux servers for instance, the /var/log/messages file(s) are 600 and owned by root. This means you need to log in to each server to review the logs or set up a zone central syslog server and forward the logs.

The [[unixsuite]] script identifies and changes the permissions so they are 644 and are group owned by the sysadmin group. This lets the unixsvc Service account retrieve the log files from all servers to be processed.

===Server Processing===

Due to the great number of messages going to the log file from local applications which was slowing down the central processing, there is a local '''chkmessages''' perl script that uses the local copy of the '''messages.exclude''' file to preprocess the log file. The output is placed in /var/tmp on the server and retrieved by the Unix service account nightly.

Note that the local copy of the '''messages.exclude''' file is server specific. You cannot use regular expressions without specifying the server name.

===Central Processing===

The central processing script uses the central '''messages.exclude''' file to post-process all the messages into a single file hosted on the web server. The central data file is more of a cross server filter. Local application specific filters should be in the server based data file. More generic sysadmin type message (like user logins) should be in the central data file.

