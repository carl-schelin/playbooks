## unixsuite Script

The **script framework** is intended to be a wrapper around several other specific scripts. The primary purpose is to make updates to 
the script and all subscripts in an efficient manner. The directory is user/group owned by the unix service account (unixsvc) and the sysadmin 
group. The directory is also not visible outside of these two users/groups (chmod 770). Being group modifiable permits quick script updates 
when changes are needed.

The script has the header block containing the description and a changelog.

There is a **runscript** function that takes a passed script name and manages running it. The function has a 5 minute timeout for all passed scripts 
and kills any processes that have been waiting longer than the timeout.

Syntax: runscript [scriptname]

The script framework is run nightly at 1am system time, so scripts are run sequentially starting at 1am. There are day of the month (DOMONTH) 
and day of the week (DOWEEK) variables so you can set up weekly or monthly script runs if daily ones are too often. Of course others can be added.

There are specific operating system sections as well to account for differences in configurations. One common task in each OS section is to ensure 
logs are configured to be viewable by any user.

One dependency is that the **chksudoers** script uses the output of **chkusers** to build its data file. So **chkusers** must run first followed 
by **chksudoers** to ensure accurate information.

It is also configured to permit unique system specific scripts. The system specific script must be named the same as the hostname of the system. There 
is also an option to run system specific scripts on a weekly basis. You'll need to set up the day of the week the script needs to be run and under that, 
the name of the script with an extension of ".weekly" to differentiate between a daily script and a weekly script in the event there are two requirements.

