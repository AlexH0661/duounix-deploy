# Duo Unix - Deploy

## Introduction
This role is designed to deploy Duo's Unix Multi Factor Authentication application, and complete a base configuration.

## Example Playbook
```yaml
playbook.yaml
---
- name: Deploy Duo Unix - Multi Factor Authentication
  hosts: all
  become: True
  vars:
    INTEGRATION_KEY: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      <integration-key>
    SECRET_KEY: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      <secret-key>
    API_HOSTNAME: api-<api-uid>.duosecurity.com
    sudo_auth: True
    ssh_auth: False
  roles:
    - duounix
```

## Example Run
```bash
ansible-playbook playbook.yaml -Kkv --ask-vault-pass
```

## Available Variables
name | default | required | affects
:--- | :--- | :--- | :---
INTEGRATION_KEY | none | True | Duo API Access
SECRET_KEY | none | True | Duo API Access
API_HOSTNAME | none | True | Duo API Access
failmode | safe | False | Duo Config
pushinfo | yes | False | Duo Config
autopush | yes | False | Duo Config
prompts | 1 | False | Duo Config
groups | none | False | Duo Config
ssh_auth | True | False | SSH MFA Config
sudo_auth | False | False | Sudo MFA Config
all_auth | False | False | System wide MFA Config

To find out more about the Duo Config, please go to https://duo.com/docs/duounix#duo-configuration-options
