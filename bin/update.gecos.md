Description: The update.gecos script updates a user's GECOS field on every server. With company emails changing from @intrado.com to @west.com or @regmail.west.com, there needed to be a way to automatically correct the user entries to prevent errors from being reported.
    
If a changefreeze (file exists) is in effect, the script exits without checking. A changelog is sent when a record is updated.

The script loops through all users on a system and compares the GECOS entry against the correct one in the valid.email file. If different, the script uses 'usermod -c' to update it.

Note that any system based account can have the GECOS record changed including service accounts. This ensures you can change "unixadmins@intrado.com" to "sfs-unix-admins@west.com" should it come to that.
 
* Location: [server]:/opt/intrado/bin/update.gecos
* Data File: [server]:/opt/intrado/etc/valid.email
* Source File: lnmt1cuomrcs1:/opt/static/intrado/etc/valid.email
* Changefreeze File: [server]:/opt/intrado/etc/changefreeze

