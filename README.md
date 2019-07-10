check_lagg_lacp
===================
Derived from https://github.com/jeanpaulgalea/check_lagg_failover 

Nagios plugin for FreeBSD lagg lacp interface.

Alert when a lagg lacp interface has failed-over to a slave port.

For more information about lagg interfaces in general;  
http://www.freebsd.org/doc/handbook/network-aggregation.html

This check is meant to serve two purposes;

1. To alert that, for some reason, a child port is not active

	This could mean that the nic card is fried,
	the upstream switch is down, etc.

2. To give the system administrator as much time as possible
	in order to bring the master port back online.

	This is especially important when the lagg interface
	is configured with only two ports.


Limitations
-----------

This plugin only works when the lagg interface is configured in "LACP Mode".
For failover see https://github.com/jeanpaulgalea/check_lagg_failover

Dependencies
------------

`nagios-plugins` must be installed from the ports tree.


Installation
------------

Copy `check_lagg_lacp` to `/usr/local/libexec/nagios/check_lagg_lacp`

Then set ownership and permissions;
```
chown root:wheel /usr/local/libexec/nagios/check_lagg_lacp
chmod 0555       /usr/local/libexec/nagios/check_lagg_lacp
```

Examples
-------

```
~$ /usr/local/libexec/nagios/check_lagg_lacp lagg0
OK - lagg0 lacp is active
~$ echo $?
0
```

```
~$ /usr/local/libexec/nagios/check_lagg_lacp igb0
WARN - igb0 is not a link lacp interface!
~$ echo $?
1
```

Testing
-------

Tested with a lagg interface consisting of two ports ("laggport"),
although it should work with any number of ports.

Tested on FreeBSD 10.3-STABLE 11.2-STABLE and 12.0.STABLE

