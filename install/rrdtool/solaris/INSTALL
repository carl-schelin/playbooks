#!/bin/ksh

cd /usr/local/bin
ln -s ../rrdtool-1.2.19/bin/rrdtool rrdtool
cd /opt/unixsuite
rm rrdtool.sparc.tar
chown -R root:root rrdtool
mkdir -p /var/rrdtool/data
mkdir -p /var/rrdtool/graphs
cd /opt/unixsuite/rrdtool
./makerrd
./makegraphs
cat README

