Description: The update.forward script adds a .forward entry pointing to WHOCARES if it doesn't exist, and then loops through the OLDFORWARD list of users and replaces it with the value in WHOCARES.
    
If a changefreeze (file exists) is in effect, the script exits without checking. A changelog is sent only when a record is updated.

* Location: [server]:bin/update.forward
* Data File: [server]:.config
* Changefreeze File: [server]:etc/changefreeze

