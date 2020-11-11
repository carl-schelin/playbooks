Description: The chkusers perl script and chkusers.contrib and chkusers.Q4 scripts parse the system passwd and shadow files. Centrify is queried as well and Centrify accounts have ',centrify' instead of the user email address in the GECOS field of the chkusers.dat file.

Output is a single colon delimited line per user consisting of:

Hostname
User Login
GECOS Field
Last time the user password was changed
Last time the user was logged in
Status of the user account

Note that the last time the user was logged in line is not provided for HP-UX systems as it's from the output of finger and the wtmpx files aren't rolled on HP-UX systems so the delay was taking an extremely long time.

* Location: [server]:bin/chkusers
* Location: [server]:bin/chkusers.contrib (HP-UX specific)
* Location: [server]:bin/chkusers.Q4 (HP-UX specific)
* Data File: [server]:var/chkusers.dat
* Process File: [management server]:admin/bin/getusers
* Full Listing: [management server]:admin/servers/chkusers.dat

The chksudoers script uses the chkusers.dat file to pull information.

The Process File retrieves the chkusers.dat file and concatenates it to a central complete Full Listing.

Note: The reason for the two HP specific scripts are due to the locations of perl. The scripts haven't changed much over time and what really should happen is the calling script should locate perl and call the script as "perl chkusers" vs having three scripts. Copious free time as always.

