Description: The chkbash script is used to check the status of the bash ShellShock vulnerability on Linux (Red Hat, CentOS, and Debian), Solaris, and HP-UX. On Red Hat and CentOS systems, the RPM is checked to see if the vulnerability has been addressed. For the rest of the systems, the associated bashvul script is executed which tries to exploit the vulnerability reporting the results.

* Location: [server]:/opt/intrado/bin/chkbash
* Data File: [server]:/opt/intrado/etc/bash.vulnerable and [server]:/opt/intrado/etc/bash.cve
* Support Script: [server]:/opt/intrado/bin/bashvul
* Data File: [server]:/opt/intrado/etc/bash.output
* Reporting Script: incojs01:/usr/local/admin/bin/processetc
* Web Page Script: bash.product
* Web Page: https://incojs01.scc911.com/reports/bash.product.php
* Web Page Script: showbash
* Web Page: https://incojs01.scc911.com/reports/bash.php
* Web Page Script: showcve
* Web Page: https://incojs01.scc911.com/reports/cve.php

The bashvul support script attempts to exploit the bash vulnerability and reports it to the bash.output data file for review.

The bash.product script creates a list of system results by Product. Any system that has a vulnerability is highlighted for the specific vulnerability.

The showbash script creates an alphabetical list of systems. Any system that has a vulnerability is highlighted for the specific vulnerability.

The showcve script creates an alphabetical list of systems with the bash version displayed. Any system that has a vulnerability is highlighted for the specific vulnerability. Note that it appears this script hasn't run since June of 2015.

