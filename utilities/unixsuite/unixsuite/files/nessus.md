Description: The nessus script ensures the nessus account has a .ssh directory in the account home directory, the directory has appropriate permissions, and installs the appropriate authorized_keys file which is created from the id_rsa.pub file, provided by InfoSec.

The nessus account is used by the Security Center software to perform a credentialed scan of a server.

* Location: [server]:bin/nessus
* Data File: [server]:etc/nessus.id_rsa.pub

