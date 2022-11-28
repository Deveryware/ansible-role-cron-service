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
