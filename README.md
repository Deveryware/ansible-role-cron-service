Role ton configure cron daemon
==============================

Ansible role to configure cron Daemon.

Informations:
-------------

This role only purpose is to configure Cron deamon not to configure cronjobs (the Ansible builtin exists for that).

Role Variables
--------------

| Variable | Description | Default |
|----------|-------------|---------|
| `cron_extra_options` | options for cron daemon | '' |
| `cron_restart_when_changed` | If True: restart cron when configuration is changed | 'true' |
| `crond_package` | Name of cron daemon package | 'cron' |
| `crond_service` | Name of cron draemon service | 'cron' |
|  ̀crond_configuration_file` | configuration file for cron daemon | '/etc/default/cron' |


Cron options
------------
Extra options for cron, see cron(8)

For ewample:
```
       -f      Stay in foreground mode, don't daemonize.

       -l      Enable  LSB  compliant  names  for  /etc/cron.d  files.  This  setting,  however,  does  not  affect  the parsing of files under /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly or
               /etc/cron.monthly.

       -n      Include the FQDN in the subject when sending mails. By default, cron will abbreviate the hostname.

       -L loglevel
               Tell cron what to log about jobs (errors are logged regardless of this value) as the sum of the following values:
                   1      will log the start of all cron jobs
                   2      will log the end of all cron jobs
                   4      will log all failed jobs (exit status != 0)
                   8      will log the process number of all cron jobs
               The default is to log the start of all jobs (1). Logging will be disabled if levels is set to zero (0). A value of fifteen (15) will select all options.
```

Example Playbook
----------------

```yaml
- name: Configure extra options for cron daemon
  hosts: fqdn
  gather_facts: true
  become: true
  vars:
    crond_extra_options: "-n"
  roles:
    - ansible-role-cron-service
  tags: ['crond']
```

```yaml
ansible-playbook -i fqdn, example_playbook.yml -D
```

Author Information
------------------

Written by Nicolas de Ferrières on the behalf of Deveryware.
