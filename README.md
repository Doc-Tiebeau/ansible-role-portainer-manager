# Portainer Manager

- [Portainer Manager](#portainer-manager)
- [Requirements](#requirements)
- [Architectures:](#architectures)
- [Role Variables](#role-variables)
- [Dependencies](#dependencies)
- [OS Bootstrap](#os-bootstrap)
  - [Flatcar Container Linux](#flatcar-container-linux)
- [Example Inventory](#example-inventory)
- [Example Playbook](#example-playbook)
- [License](#license)
  - [Author Information](#author-information)

Ansible-role-portainer-manager aims to deploy, configure and manage Portainer ecosystems.

# Requirements

This role requires:
 - Ansible minimum version: 2.10.12
 - Ansible inventory structure: YAML
 - Python Jmespath
   - ```
      pip install jmespath
      ```

# Architectures:

Tested on:
- Alpine Linux 3.15
- Debian 10
- Ubuntu 20.04
- RedHat 8
- CentOS 8

# Role Variables

See inventory

# Dependencies

```yaml
  - roles:
    - # none
  - collection:
    - name: community.docker
      version: <= 1.7.0
      source: https://galaxy.ansible.com
```
# OS Bootstrap
## Flatcar Container Linux

Because Flatcar Container Linux is delivered on immutable file system, it needs specific customization to work with ansible and wir portainer manager too.

This section is adapted from [kubespray's flatcar bootstrap](https://github.com/kubernetes-sigs/kubespray/blob/6aac59394e5d2801e4dcde71c393b73201a880ef/roles/bootstrap-os/tasks/bootstrap-flatcar.yml).

Following components are missing on Flatcar:
 - Python 3 (pypy v3.6 or later) (see [bootstrap.sh](contrib/flatcar/bootstrap.sh))
 - Python PiP ( see contrib playbook [bootstrap-flatcar.yml](contrib/flatcar/bootstrap-flatcar.yml))
 - Python-Docker (even if docker is already present in system see contrib playbook [docker-flatcar.yml](contrib/flatcar/docker-flatcar.yml))
   - Do not try to install pip using pypy on Flatcar, its fails.
 - Docker-Compose (2.1.1 or later) (see contrib playbook [docker-flatcar.yml](contrib/flatcar/docker-flatcar.yml))
   - Need to be `/opt/bin/docker-compose`


**Note**: Because of unexpected side effects locksmithd auto upgrade and reboot service is disabled at this time.

# Example Inventory

```yaml
all: # keys must be unique, i.e. only one 'hosts' per group
  hosts:
    master01:
      ansible_host: <master_IP|FQDN>
      ansible_user: <ssh_login>
      ansible_ssh_pass: <ssh_password>
      # ansible_ssh_args: '-o StrictHostKeyChecking=no' # Uncomment this line to bypass prompt for ssh key validation, use at your own risk !!!
      apps:
        docker: # Optional: activates installation without confirmation
          portainer:
            version: 2.9.3 # MANDATORY: digits only
            type: master # MANDATORY: master or docker-slave (portainer_agent)
            address: <IP|FQDN> # Optional: Portainer URL without <http://> and <port>; default <ansible_host>
            port: <digit> # Optional: default 9000
            login: <portainer_admin_login> ## Optional: default: admin
            password: <portainer_admin_password> #default: Test1234
            endpoints: # Optional: Register endpoints after portainer installation
              - Name: master01 # local server where portainer has been deployed
                Type: master # MANDATORY: master or docker-slave (portainer_agent)
                EndpointCreationType: 1
                URL: "unix:///var/run/docker.sock"
                PublicURL: <IP|FQDN> # Optional but recommended to get shortcuts functional in portainer API
              - Name: slave<NN> # remote server which docker API has been opened
                Type: docker-slave # MANDATORY: master or docker-slave (portainer_agent)
                EndpointCreationType: 1
                URL: "tcp://<IP|FQDN>:<port>" # default tcp port is 2375
                PublicURL: <IP|FQDN> # Optional but recommended 
    node02:
      ansible_host: <master_IP|FQDN>
      ansible_user: <ssh_login>
      ansible_ssh_pass: <ssh_password>
      # ansible_ssh_args: '-o StrictHostKeyChecking=no' # Uncomment this line to bypass prompt for ssh key validation, use at your own risk !!!
      apps:
        docker: # Optional: activates installation without confirmation
          portainer:
            version: 2.9.3 # MANDATORY: digits only
            type: docker-slave # MANDATORY: master or docker-slave (portainer_agent)
            mode: portainer_agent # MANDATORY: only portanier_agent supported at this time
```

# Example Playbook

After formating and populating your **YAML** inventory add following inside your playbook.

```yaml
  roles:
    - role: ansible-role-portainer-manager
      when: hostvars[inventory_hostname].apps.docker.portainer is defined
```

# License

GNU GPL-V3  
Free of use, modify and redistribute.

Distribute with same LICENSE (or less restrictive).

Should probably comes in CC BY-SA for future versions.

Author Information
------------------

Jack of all trades master of none.
