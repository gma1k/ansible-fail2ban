# ansible-fail2ban

Install fail2ban package.

## Requirements

This role requires Ansible 2.5 or higher.

* Role Variables
* Default Role Variables
* Package variables

```
fail2ban_packages :
  - name: 'fail2ban'
```

# Service variables

```
fail2ban_service_name: 'fail2ban'
```
# Main configuration

```
fail2ban_main_config_content:
  - option: 'loglevel'
    value: 3
  - option: 'logtarget'
    value: '/var/log/fail2ban.log'
  - option: 'syslog-target'
    value: '/var/log/fail2ban.log'
  - option: 'syslog-facility'
    value: 1
  - option: 'socket'
    value: '/var/run/fail2ban/fail2ban.sock'
  - option: 'pidfile'
    value: '/var/run/fail2ban/fail2ban.pid'
```

# Jails configuration

```
fail2ban_jails:
  DEFAULT:
    backend: 'systemd'
    ignoreip: '127.0.0.1/8 ::1 10.0.0.0/8'
    banaction: 'firewallcmd-rich-rules[actiontype=<multiport>]'
    banaction_allports: 'firewallcmd-rich-rules[actiontype=<allports>]'
  ssh:
    enabled: true
    port: 'ssh'
    filter: 'sshd'
    logpath: '/var/log/secure'
    maxretry: 3
    findtime: 600
```
## Example playbook 

```
- hosts: servers
  roles:
    - { role: ansible-fail2ban }
```
