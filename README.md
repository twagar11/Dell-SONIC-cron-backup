# Dell-SONIC-cron-backup

## Description and Objective

This small repo is indended to provide a simple way to schedule weekly backups of all your Dell SONiC switches using a simple Ansible playbook and schedule using a cron job which runs from the Linus ansible node

## Requirements

  The intention of this repo is to provide a working example to use as a building block within your own automation infrastructure.  A sample directory structure as well as code versions are included.  It is assumed the use of this repo will modify for you specific environment.

  GNS3 virtualization was used for Ansible node and Dell Sonic switches
  
  Ansible node = Ubunutu 18.04
  
  Python = 3.6.9
  
  Asnible = 2.10.11
  
  Dell SONiC = 3.2
  
  Dell SONiC latest collections can be installed from Ansible Galaxy
  
  ansible-galaxy collection install dellemc.enterprise_sonic
  
  Ansible.netcommon = 2.2.0
  
  Asnible.utils = 2.3.0
  
  Dellemc.enterprise_sonic = 1.1.0
  
Sample Ansible node directory structure

gns3@gns3:/home/labuser/module1/Scripts$ tree
.
├── backup
│   ├── Switch1
│   │   └── switch.json
│   └── Switch2
│       └── switch.json
├── group_vars
│   └── oldall
├── group_vars.yaml
├── host_vars
│   ├── Switch1.yaml
│   └── Switch2.yaml
├── inventory.yaml
├── pb_backup.yaml
└── templates
    └── clis.j2

## Phase 1 (Create Backup Playbook and Schedule weekly execution with cron)

Ansible playbook = pb_backup.yaml

Ansible inventory = inventory.yaml

Execution (run from ../Scripts/ ) = ansible-playbook -i inventory.yaml pb_backup.yaml

Dell SONiC switch running-config is stored on switch /etc/sonic/config_db.json

First part of playbook will loop and make a copy of the config_db.json on every switch /home/admin/switch.json

Second part will copy switch.json to Ansible node, create "backup/" directory and switch hostname subdirectories for each switch

Crontab -e is used to edit user specific cron job to schedule pb_backup.yaml playbook to run every sunday at midnight

***** As of 1/19/24 Ubuntu cron scheduler recieves MTA not installed error and does not execute ******


## Phase 2 (Create Restore Playbook to push backup json to switch)

TBD

