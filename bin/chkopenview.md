Description: The chkopenview script sends a Minor test message to the Openview server to verify monitoring is working.

I added the ovmc account to the Unix Admins group back in 2009 in order to capture statistics. In 2014, I started importing the alarms into the Inventory to associate them with the appropriate servers. In 2018 I created this script with input from the Monitoring team in order to ensure alarming was working. Since mid 2017 there had been several instances of no alarms being received by the team for production systems.

The belief was that during incidents, events, changes, or even after a system or product went live, that monitoring had been disabled and reenabling alerting had not occurred. In discussion with other teams, it was confirmed that they had received alarms for systems the Unix team had not so getting a loop in place would let the team be aware of a few systems where alarming might not be enabled.

The Health Report in the Inventory shows every server that has not received an alarm in the past 5 days which includes test alarms which have been sent out several times over the past 8 months.

* Location: [server]:bin/chkopenview
* Data File: [server]:var/chkopenview.output
* Email: ovmc@[management server]
* Inventory Input: [management server]:/usr/local/httpd/bin/alarms.submit.php
* Process Script: [management server]:/export/home/ovmc/Mail/process
* Health Report: https://[inventory server]/reports/ovmessages.php?group=1&product=0

