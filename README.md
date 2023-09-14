# quick and dirty Munin plugins
You'll probably need to change these to fit your needs.

## apcupsd_multi
graphs:

- percentages
- runtime
- volts
- est. watts

dependencies: apcaccess

## elasticsearch_indices
graph indices by

- document count
- size
- status

## fail2ban
graphs: currently banned count by jail

dependencies: fail2ban-client

### plugin config
	[fail2ban]
	env.jails jail1 jail2 jailn

## snmp_mikrotik
use these like any snmp plugins:

	ln -s /whereever/snmp__mikrotik_cpu /etc/munin/plugins/snmp_My.Host.com_mikrotik_cpu
	### munin.conf ###
	[My.Host.com]
	address 127.0.0.1
	use_node_name no

link snmp__mikrotik_storage as snmp_HOST_mikrotik_mem or _disk

dependencies: snmpget

### plugin config
	[snmp_HOST_mikrotik_*]
	env.snmpopts -l authNoPriv -u MyUser -a SHA -A MyPassword -r 2
	env.numcpu 4
	env.iflist		# leave empty/unset: dynamically find and name all interfaces
	env.iflist 2 3 5	# only show interfaces 2 3 5
	env.iflist eth1 eth2	# show ifs 1, 2 and name them eth1, eth2 - these have to be in order and start at if 1. Saves traffic and exectime	
	env.storageID 65536	# this one is optional, when linked as _mem oder _disk, it will set a default OID. Set if your storage has a different id.

## squid 
dependencies squidclient

### plugin config
	[squid_*]
	env.squidhost 127.0.0.1
	env.squidport 3128
