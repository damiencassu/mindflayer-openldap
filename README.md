Mindflayer OpenLdap
=========

A simple Ansible role to deploy and manage OpenLDAP 2.5 (LTB) on CentOS9/RHEL9

The deployed OpenLDAP package will be the one provided by the LDAP Tool Box (LTB) project (see https://www.ltb-project.org for more details)

Requirements
------------

This role has been tested with Ansible 2.14.13

This role must be executed with root privileges

Role Variables
--------------

To run this role, you must specify in the vars section of your playbook which mode(s) to execute.

Available modes are:

* INSTALL : Will install a raw OpenLDAP 2.5 (LTB) service on the targeted host(s) =>  set the do_install variable to true
* UNINSTALL : Will uninstall OpenLDAP 2.5 (LTB) service on the targeted host(s) by undoing INSTALL tasks => set the do_uninstall variable to true 

You will find below the list of all variables used by this role (defined in defaults/main.yml) along with their default value if not overridden.

For each variable, the mode(s) by which the variable is used is(are) listed.

_For instance, ltb_repo_baseurl is used when executing INSTALL tasks (when do_install is set to true)_

| Mode | Variable name | Default value | Description |
| ---- | ------------- | ------------- | ----------- |
| INSTALL | ltb_repo_baseurl | https://ltb-project.org/rpm/openldap25/$releasever/$basearch | LTB Repo base url to configure in yum repo file |
| INSTALL/UNINSTALL | ltb_repo_gpgkey | file:///etc/pki/rpm-gpg/RPM-GPG-KEY-LTB-project | Local path where the LTB Repo GPG key is stored |
| INSTALL | ltb_repo_remote_gpgkey | https://ltb-project.org/documentation/\_static/RPM-GPG-KEY-LTB-project | Remote URL where the LTB Repo GPG key can be downloaded |
| INSTALL/UNINSTALL | base_dir | /tech/openldap | Root directory tree name where slapd directories will be created |
| INSTALL | data_dir | data | Name of the directory which will contain slapd mdb database |
| INSTALL/UNINSTALL | log_dir | log | Name of the directory which will contain slapd log files |
| INSTALL/UNINSTALL | backup_dir | backup | Name of the directory which will contain slapd backups |
| INSTALL/UNINSTALL | log_file | slapd.log | Name of the slapd log file |
| INSTALL | backup_retention_days | 7 | Number of days to keep old backups before their deletion |
| INSTALL/UNINSTALL | backup_cron_month | * | Month cron metric to configure slapd conf and data backup scheduling |
| INSTALL/UNINSTALL | backup_cron_day | * | Day cron metric to configure slapd conf and data backup scheduling |
| INSTALL/UNINSTALL | backup_cron_weekday | * | Weekday cron metric to configure slapd conf and data backup scheduling |
| INSTALL/UNINSTALL | backup_cron_hour | 03 | Hour cron metric to configure slapd conf and data backup scheduling |
| INSTALL/UNINSTALL | backup_cron_minute | 00 | Minute cron metric to configure slapd conf and data backup scheduling |


Dependencies
------------

Only Ansible builtin modules are unsed in this role.

Example Playbook
----------------

To launch installation tasks on localhost

```
- hosts: localhost
  vars:
   - do_install: true
   - do_uninstall: false
  roles:
   - mindflayer-openldap
```

To launch uninstallation tasks on localhost

```
- hosts: localhost
  vars:
   - do_install: false
   - do_uninstall: true
  roles:
   - mindflayer-openldap
```


License
-------

MIT - See dedicated LICENSE file for details

Author Information
------------------

Damien CASSU

Official GitHub repository for this role: https://github.com/damiencassu/mindflayer-openldap
