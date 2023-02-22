Install the rrdtool package
rpm --install rrdtool-1.2.27-3.el4.i386.rpm

Install the script package
mv rrdtool.linux.tar /usr/local
tar fvx rrdtool.linux.tar
chown -R unixsvc:sysadmin rrdtool
chmod -R g+w rrdtool

Next create the data directory
mkdir -p /var/rrdtool/data
mkdir /var/rrdtool/graphs

Update the config file with the interfaces and drive information.

Interfaces:
This is the name of the function to be used to create the graphs and thumbnails. The function should exist. If not, take a current one and dup it to make the updates.
1. Run ifconfig -a to see which interfaces are configured
2. That the interface bit in makerrd creates the database for eth0; remove the unnecessary entries.
3. That the interface bit in updaterrd only updates the eth0 part of the databases.
4. That the makegraphs script has the eth0 function
5. That the makethumbs script has the eth0 function (if it's in makegraphs, it should be in makethumbs but check anyway).

Drives:
This is the function name again along with the usage and label if appropriate. So if it's "sda:root:WWID" the graph would use the sda function, the title would be /dev/sda (root) and would also contain the WWID if it's part of the variable.
1. Run iostat -dx to see what drives are available.
2. Check and update makerrd for the appropriate drive
3. Check and update updaterrd for the appropriate drive
4. Make sure the function you're using exists in makegraphs
5. Make sure the function you're using exists in makethumbs.

Disks:
This is a list of the disk label names and rrd database label names. The diskg function will use this to extract data from the database so the label here needs to match the label used in the rrd database.
1. Check and update makerrd to add or remove necessary drive labels.
2. Check and update updaterrd again for the correct drives.

Next check the number of CPUs in the system and make adjustments to makerrd, makegraphs, makethumbs, and updaterrd
mpstat -P ALL

Run the database creation script; This makes all the rrd database.
./makerrd

Update root's cron to add the following lines

# monitor rrdtool
*/5 * * * * /opt/unixsuite/rrdtool/watchrrd > /dev/null 2>&1

# generate rrdtool graphs
*/15 * * * * /opt/unixsuite/rrdtool/makegraphs > /dev/null 2>&1

