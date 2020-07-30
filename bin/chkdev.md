## chkdef Script

Description: The **chkdef** script lists all the defunct processes in the system. This was initially created to identify systems where a bug 
with OpenView caused there to be 2 defunct processes. In the mean time, we found one of the database servers would have a perl script that 
failed to exit cleanly leaving 45 or so defunct processes. A webpage report of the processes plus a report in the status email that count the 
number of defunct processes is created. The status email also creates a status web page which lists all issues including a defunct process count.

* Location: [server]:/opt/intrado/bin/chkdef
* Data File: [server]:/opt/intrado/etc/defunct.data
* Reporting Script: incojs01:/usr/local/admin/bin/processetc
* Web Script: incojs01:/usr/local/admin/bin/showdef
* Web Page: [https://incojs01.scc911.com/reports/defunct.php](https://incojs01.scc911.com/reports/defunct.php)
* Email Script: incojs01:/usr/local/admin/bin/status.email
* Email Script: incojs01:/usr/local/admin/bin/status.email.tandem
* Status Web Page: [https://incojs01.scc911.com/status](https://incojs01.scc911.com/status)

Note that the **chkserver** script does list a count of defunct processes but doesn't list them since there may be quite a few.

