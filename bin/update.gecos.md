Description: The update.gecos script updates a user's GECOS field on every server. With company emails changing from @OLDADDR to @NEWADDR, there needed to be a way to automatically correct the user entries to prevent errors from being reported.
    
If a changefreeze (file exists) is in effect, the script exits without checking. A changelog is sent only when a record is updated.

The script loops through all users on a system and compares the GECOS entry against the correct one in the valid.email file. If different, the script uses 'usermod -c' to update it.

Note that any system based account can have the GECOS record changed including service accounts. This ensures you can change the "ADMINS@OLDADDR"" to "ADMINS@NEWADDR" should it come to that.
 
* Location: [server]:bin/update.gecos
* Data File: [server]:etc/valid.email
* Source File: lnmt1cuomrcs1:etc/valid.email
* Changefreeze File: [server]:etc/changefreeze

