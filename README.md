18-ANSIBLE-DNF-INSTALL/
├── inventory
├── create_scripts_dir.yml
└── README.md


# =========================
# inventory
# =========================
[dev_fs]
dev-1
dev-2


# =========================
# create_scripts_dir.yml
# =========================
---
- name: create shared scripts directory
  hosts: dev_fs
  become: yes

  vars:
    username: fshelton

  tasks:
    - name: create directory for scripts
      file:
        path: "/opt/scripts/{{ username }}"
        state: directory
        owner: "{{ username }}"
        group: webmasters
        mode: '0775'


# =========================
# README.md
# =========================
# 18. ANSIBLE DNF INSTALL

## Overview
This project demonstrates the use of Ansible to automate system configuration across multiple servers.

## Task
Create a shared directory on multiple development servers with proper ownership, group, and permissions.

## Configuration
- Directory: /opt/scripts/fshelton
- Owner: fshelton
- Group: webmasters
- Permissions: 775

## Playbook Details
The playbook targets multiple hosts defined in the inventory file and uses privilege escalation to perform system-level changes.

## Execution
Run the playbook using:

ansible-playbook -i inventory create_scripts_dir.yml -K

## Validation
Verify the directory on target systems:

ls -ld /opt/scripts/fshelton

Expected output:
- Owner: fshelton
- Group: webmasters
- Permissions: drwxrwxr-x
