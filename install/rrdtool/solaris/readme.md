# monitor rrdtool
0,5,10,15,20,25,30,35,40,45,50,55 * * * * /opt/unixsuite/rrdtool/watchrrd > /dev/null 2>&1

# generate rrdtool graphs
0,15,30,45 * * * * /opt/unixsuite/rrdtool/makegraphs > /dev/null 2>&1

