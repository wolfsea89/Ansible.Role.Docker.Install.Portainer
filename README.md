Ansible.Role.Docker.Install.Portainer
=========

The role that installs and configures portainer.

Language: [EN](README.md), [PL](README.PL.md)


Role Variables
--------------
requires:
```
  docker:                   # Docker configuration
  configuration:            # Traefik configuration
  domain:                   # Domain configuration
  users:                    # List of all users declared in inventory - Preferred place group_vars / all
  users_in_docker:          # List of users to be declared on the docker services
  install_container:        # Do you want to install a container? << true | false >>
  configuration_container:  # Do you want configurure service (CaaC) << true | false >>
```

example `docker`recommended in `group_vars`
```
docker:
  docker_compose_dir: /Data/containers
  docker_volumens_dir: /Data/containers
```
example `configuration` recommended in `group_vars`

[egxample](roles/Ansible.Role.Docker.Install.Portainer/tests/inventory)

example `sites` recommended in `host_vars`
```
  portainer:
    domain_name: portainer.rachuna.pl
    url: "https://portainer.rachuna.pl"
```
example `users_in_docker` recommended in `host_vars`
```
  users_in_docker:
    - name: administrator
      docker_services:
        - portainer
```
example `users` recommended in `group_vars/all`
```
 users:
    - name: Administrator 
      username: administrator
      default_password: "aaa"
      state: present
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```
- name: Install all containers
  hosts: localhost
  become: true
  gather_facts: no
  roles:

    - role: Ansible.Role.Docker.Install.Portainer
      tags: [portainer, docker, install]
      vars:
        docker:
          docker_compose_dir:  /Data/containers
          docker_volumens_dir: /Data/containers 
        # configuration:     <- tests/inventory
        # domains:           <- tests/inventory
        # user_in_docker:    <- tests/inventory
        users: # Recommendation: Defining in group_varss/all
          - name: Administrator
            username: administrator
            default_password: "aaa"
            state: present
        install_container: true
        configuration_container: true
      when:
        - "'portainer' in system.docker_services"
```

Testing
------------

Testing on:
  - Ubuntu 16.04 LTS
  - Ubuntu 18.04 LTS
  - Ubuntu 20.04 LTS
  - Centos 7
  - Centos 8

License
-------

BSD

Author Information
------------------
 **Maciej Rachuna**
##### System Administrator & DevOps Engineer
rachuna.maciej@gmail.com
