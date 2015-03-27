# internet-fo
Route switching Internet failover script for Debian servers

This is for those cases where bonding is not an option,
because the link on the interface doesn't goes down on failure.

It can be started from Cron or Heartbeat. A check script tries to reach
Google's DNS server (8.8.8.8) with ICMP packets many times.
In case of failure, it switches the default route to the backup line.

It is possibile to change the check script, if you want to test failure
in an other way.
