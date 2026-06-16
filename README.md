# zabbix-templates
Personal Zabbix Templates, will be adding more as time allows.  Templates exported from a Zabbix 7.0 system, I will not be doing templates for older versions. Mostly Windows-centric templates and designed around running inline Powershell commands via system.run rather than external scripts for environments where you may not have an easy way to stage external scripts on your remote hosts.  Note that using AllowKey=system.run[*] can be considered a security risk, so use at your own peril.

unifi_cloud__http.yaml - This differs a bit from existing community templates as it does not use/depend on local network access.  It uses an API key generated via api.ui.com and then makes one call to /v1/sites to get gateway id's then makes a call to /v1/devices per site using the previously discovered id's to filter the device list.  Tested with a 4 site setup with single gateways at each site.  Built using Zabbix 8.0.0beta1 but should work on 7.x.

dhcp_scope_statistics.yaml - Discovers and monitors DHCP scopes via a system.run item with the domain passed via host macro, no external scripts.

exchange_component_health.yaml - Discovers and monitors Exchange Components via a system.run item, no external external scripts.  Includes host macros to filter out/exclude specific components.

wsfc_monitoring.yaml - Very basic template to monitor health of Windows Server Failover CLuster nodes and alert if number of down nodes exceeds a threshold.  Threshold is configured via Host Macro.  Recommend creating a "dummy" host in Zabbix and adding agent interface for each cluster node individually to this host.  This prevents duplicate alerts from every node when an alert fires and should allow it to function as long as at least one node is up.

dell_storage_center_snmp - Loosely based on https://github.com/asosso/zbx3-dell-compellent but largely rebuilt from ground up.  Tested on Dell/Compellent OS 07.04.10.027 with EN-SCv3020 enclosures
