nxos_prepare
=========
[![Build Status](https://travis-ci.org/robertwatson3/nxos_prepare.svg?branch=master)](https://travis-ci.org/robertwatson3/nxos_prepare)
This role enables NXAPI, saves running config to startup config, saves running config to bootflash, and saves running config to local machine. When any other roles are complete, NXAPI can then be disabled using a handler.

Requirements
------------

- Ansible 2.0
- pexpect (pip install pexpect)
- nxos-ansible (git clone https://github.com/jedelman8/nxos-ansible.git)

Role Variables
--------------
```YAML
bootflash_conf_file: Path/name of config backup file created on switch bootflash.
running_conf_file: Path/name of config backup file created on local machine.
running_config_dir: Path of config backup directory on local machine.
overwrite_bootflash_config: Removes existing config back on bootflash if true.
disable_nxapi: If true, disables NXAPI when playbook run is complete.
backup: If false, config is not written, and no copies are made on switch or local machine. 
```

Example Playbook
----------------
```YAML
---
- hosts: nxos
  connection: local
  gather_facts: yes
  force_handlers: True

  vars:
    config_backup_path: "bootflash:/configs/config_backup.cfg"
    backup: True
    disable_nxapi: False

  vars_prompt:
    - name: switch_username
      prompt: "What is the switch username?"
      private: False
    - name: switch_password
      prompt: "What is the switch password?"

  roles:
    - nxos_prepare
```
License
-------

BSD

Author Information
------------------

Bobby Watson (bwatsoni@cisco.com, robertwatson3@gmail.com)
