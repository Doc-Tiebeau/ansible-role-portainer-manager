ansible-role-portainer-manager
=========

Ansible-role-portainer-manager aims to deploy, configure and manage Portainer ecosystems.

Requirements
------------

This role requires:
 - Ansible version: 2.10.12
 - Ansible inventory structure: YAML
 - Python Jmespath
   - ```
      pip install jmespath
      ```

Architectures:
--------------
Tested on:
- Alpine Linux 3.14
- Debian 10
- Ubuntu 20.04
- RedHat 8
- CentOS 8

Role Variables
--------------

See inventory

Dependencies
------------

```yaml
  - roles:
    - # none
  - collection:
    - name: community.docker
      version: <= 1.7.0
      source: https://galaxy.ansible.com
```

Example Inventory
----------------
```yaml
all: # keys must be unique, i.e. only one 'hosts' per group
  hosts:
    master01:
      ansible_host: <master_IP|FQDN>
      ansible_user: <ssh_login>
      ansible_ssh_pass: <ssh_password>
      # Uncomment the following line to bypass prompt for ssh key validation, use at your own risk !!!
      # ansible_ssh_args: '-o StrictHostKeyChecking=no'
      apps:
        docker: # Optional: activates installation without confirmation
          portainer:
            address: <IP|FQDN> # Optional: Portainer URL without <http://> and <port>; default <ansible_host>
            port: <digit> # Optional: default 9000
            login: <portainer_admin_login> ## Optional: default: admin
            password: <pportaine_admin_password> #default: Test1234
            endpoints: # Optional: Register endpoints after portainer installation
              - Name: local # local server where portainer has been deployed
                EndpointCreationType: 1
                URL: "unix:///var/run/docker.sock"
                PublicURL: <IP|FQDN> # Optional but recommended to get shortcuts functional in portainer API
              - Name: master01 # remote server which docker API has been opened
                EndpointCreationType: 1
                URL: "tcp://<IP|FQDN>:<port>" # default tcp port is 2375
                PublicURL: <IP|FQDN> # Optional but recommended
```

Example Playbook
----------------

After formating and populating your **YAML** inventory add following inside your playbook.

```yaml
  roles:
    - role: ansible-role-portainer-manager
      when: hostvars[inventory_hostname].apps.docker.portainer is defined
```

License
-------

GNU GPL-V3  
Free of use, modify and redistribute.

Distribute with same LICENSE (or less restrictive).

Should probably comes in CC BY-SA for future versions.

Author Information
------------------

Jack of all trades master of none
