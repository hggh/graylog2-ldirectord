
graylog2-ldirectord
===================

Check script for ldirectord (ipvsadm/LVS) for Graylog2. If you use ldirectord with Linux Virtual Server, you have to check if your Graylog2 Server instance is running and processing of messages is enabled. (Only Graylog2 **> 0.20-rc1**)

ldirectord works with external scripts, but this does an fork every time ldirectord checks the health of an real server. That's why this script works as ```checktype=external-perl```.

Installation
----------------
 * Installation of Perl libraries: ```apt-get install libjson-xs-perl libconfig-general-perl```
 * cp etc/graylog2-ldirectord.conf /etc/graylog2-ldirectord.conf
 * create an username in your Graylog2 Instance (reader)
 * copy bin/graylog2-ldirectord to /usr/local/bin/graylog2-ldirectord

Configuration
-----------------------

 * configure ldirectord (**/etc/ldirectord.cf**):
 > virtual=192.168.100.1000:12201
 >      real=10.10.0.2:12201 masq
 >      real=10.10.0.3:12201 masq
 >      protocol=udp
 >      scheduler=rr
 >      checkcommand=/usr/local/bin/graylog2-ldirectord
 >      checktype=external-perl


This script checks if Graylog2 responds within time (default: 1s) and if node is enabled for processing log files.

