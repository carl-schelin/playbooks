## chkdef Script

Description: The **chkdef** script lists all the defunct processes in the system. This was initially created to identify systems where a bug 
with OpenView caused there to be 2 defunct processes. In the mean time, we found one of the database servers would have a perl script that 
failed to exit cleanly leaving 45 or so defunct processes. A webpage report of the processes plus a report in the status email that count the 
number of defunct processes is created. The status email also creates a status web page which lists all issues including a defunct process count.

* Location: [server]:bin/chkdef
* Data File: [server]:var/defunct.data
* Reporting Script: [management server]:admin/bin/processetc
* Web Script: [management server]:admin/bin/showdef
* Web Page: https://[management server]/reports/defunct.php
* Email Script: [management server]:admin/bin/status.email
* Email Script: [management server]:admin/bin/status.email.[groupname]
* Status Web Page: https://[management server]/status

Note that the **chkserver** script does list a count of defunct processes but doesn't list them since there may be quite a few.

