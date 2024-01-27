Zabbix template for monitoring APT package updates.

This template uses `-s` simulation option when invoking `apt-get`, so no root access is needed for Zabbix user during polling.

# Installation
1. Create a `cron` entry (see below)
2. Copy `zabbix_agentd.d/apt.conf` to the Zabbix agent's configuration directory (usually located in `/etc/zabbix`).
3. Import `templates/apt-updates.xml` to Zabbix frontend.

# Changes in this Fork
Use a dedicated cron entry like the following for the `zabbix` user (every 8 hours):

```bash
0 8,16 * * *	apt-get -s upgrade > /tmp/apt.log
```

With the old method the request was very likely to timeout. I Also added an item key to show the list of upgradeable pakets.

I also added an item with the list of packets to be upgraded. You can reach it also from the trigger values when a problem occurs.
