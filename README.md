# Bones System Ansible Roles and Playbooks

This is just a series of Ansible roles I use for my own systems. I will update these periodically as they're fleshed out. I haven't touched them for a while, so are a bit stale. It's been on my TODO list for quite a while.

These roles are currently only tested against Debian specifically, but should work on derivatives such as Ubuntu, Mint, etc.

## Current Roles

I'm not sure I like the current organization of these. They're basically defined based on the intended "roles" a system would fulfill, which is usually managed by a combination of playbook and inventory file directives. Based on current prerequisites, I likely need a role specifically to set up Let's Encrypt for shared use between dependent roles.

* `common` - Stuff I install on everything.
  - Utilities such as nano, less, rsync, etc.
  - An overloaded prompt for environment safety.
  - Environment settings I've come to enjoy.
* `docker` - Sets up the latest Docker CE on defined hosts.
* `firewall` - System lockdown settings and utilities.
  - `fail2ban` - Lock out IPs from infiltration attempts.
  - Adds iptables firewall rules to preemptively lock out traffic from China and Lithuania because something like 90% of all hack attempts come from these regions. This should probably be updated to use nftables instead.
* `smtp-server` - All necessary services to run a Postfix + Dovecot SMTP server. Most configuration pending.
  - Additional configuration necessary to secure Postfix and Dovecot using fail2ban.
  - Sets up Postgrey to whitelist domains specified in `whitelist_clients` host variable.
  - Still pending: Postfix and Dovecot config, Let's Encrypt automation.
* `webserver` - Sets up a Lighttpd server with multi-site hosting.
  - Installs Hugo for site building based on `hugo_version` variable.
  - Should work with any document root in `/var/www/DOMAIN/htdocs`
  - Needs Let's Encrypt in conjunction with `smtp-server` role somehow.
  - VERY WIP, DO NOT USE

## Pending Roles

* `proxmox` - Role to bootstrap a Proxmox server.
  - I have made several of these servers in the past.
  - I need some way to standardize deployment.
