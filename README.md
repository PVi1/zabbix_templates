# zabbix_templates
Zabbix templates:

1. HP c7000 chassis SNMP monitoring template with autodiscover

Install guide:
1. Create Regexp in Zabbix accrding to HP_regexp.png screenshot from this repository

2. Add required MIB files to your system:
I have downloaded required mibs from here: 

http://downloads.hpe.com/pub/softlib2/software1/pubsw-linux/p1580676047/v124934/upd10.50mib.tar.gz
and used mainly:

-rw-r--r-- 1 root root  98745 jún 26 15:04 cpqhost.mib

-rw-r--r-- 1 root root 270427 jún 26 15:04 cpqrack.mib

-rw-r--r-- 1 root root     73 jún 26 15:04 rfc-1212.mib

-rw-r--r-- 1 root root 105462 jún 26 15:04 rfc1213.mib

-rw-r--r-- 1 root root   3776 jún 26 15:04 rfc-1215.mib



  Based on:
  http://net-snmp.sourceforge.net/wiki/index.php/TUT:Using_and_loading_MIBS

  Steps for Ubuntu 16.04 LTS:
  1. Copy MIBs to /usr/share/snmp/mibs and rename them to SOMENAME-MIB.my
  2. EDIT /etc/snmp/snmp.conf and add mibs loading:

  mibs +CPQHOST-MIB 
  mibs +CPQRACK-MIB

  3. Restart snmpd daemon:

  /etc/init.d/snmpd restart

  Test functionality:
  snmptranslate -IR -On cpqRackServerBladePartNumber.1

  4. Restart Zabbix server to use newly added MIBS

  /etc/init.d/zabbix-server restart
  
3. Import template to zabbix
4. Create macro in zabbix:
{$COMMUNITY} - community string for chassis.


