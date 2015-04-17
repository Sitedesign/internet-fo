# internet-fo
Route switching Internet failover script for Debian servers

This is for those cases where bonding is not an option,
because the link on the interface doesn't goes down on failure.

It can be started from Cron or Heartbeat. A check script tries to reach
Google's DNS server (8.8.8.8) with ICMP packets many times.
In case of failure, it switches the default route to the backup line.

It is possibile to change the check script, if you want to test failure
in an other way.

## Getting started

### Requirements

Root access required to modify ethernet interface states.
Tested on Debian 7 (Wheezy).

### Install

Execute from shell:
```
git clone https://github.com/Sitedesign/internet-fo.git
cd internet-fo
mkdir /etc/internet-fo
cp resolv.conf.* /etc/internet-fo/
cp internet-fo.conf /etc/internet-fo/
cp internet-fo /usr/local/bin/
cp internet-fo-check /usr/local/bin/
```

### CRON based execution

In this case we run the internet-fo script in exact periods from CRON.
```
cat << EOT >/etc/cron.d/internet-fo
# /etc/cron.d/internet-fo: crontab fragment for internet-fo

# Run internet-fo every 5 minutes
*/5 * * * *   root   if [ -x /usr/local/bin/internet-fo ]; then /usr/local/bin/internet-fo >/dev/null 2>&1; fi
EOT
/etc/init.d/cron reload
```

### Heartbeat based execution

If you have a HA cluster with Heartbeat, you can run the internet-fo on cluster change event.

Add internet-fo to /etc/ha.d/haresources and create a script with internet-fo name in /etc/ha.d/resource.d.

## License
Copyright (c) 2015 Krisztian CSANYI Licensed under the GPLv2 license.
