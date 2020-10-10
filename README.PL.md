Ansible.Role.Docker.Install.Portainer
=========

Rola instalująca i konfigurująca portainer.

Język: [EN](README.md), [PL](README.PL.md)


Zmienne w roli
--------------
requires:
```
  docker:                   # Potrzebna konfiguracja dockera
  configuration:            # Konfiguracja traefika
  domain:                   # Konfiguracja domeny
  users:                    # Lista wszystkich użytkowników zdeklarowanych w inventory - Preferowane miejsce group_vars/all
  users_in_docker:          # Lista użytkowników do zdeklarowanych na serwisach docker`owych
  install_container:        # Czy instalować od nowa kontener?        << true | false >>
  configuration_container:  # Czy konfigurować konter za pomocą CaaC? << true | false >>
```

przykład `docker` zalecane w `group_vars`
```
docker:
  docker_compose_dir: /Data/containers
  docker_volumens_dir: /Data/containers
```
example `configuration` zalecane w `group_vars`

[egxample](roles/Ansible.Role.Docker.Install.Portainer/tests/inventory)

example `domain` zalecane w `host_vars`
```
  portainer:
    domain_name: portainer.rachuna.pl
    url: "https://portainer.rachuna.pl"
```
example `users_in_docker` zalecane w `host_vars`
```
  users_in_docker:
    - name: administrator
      docker_services:
        - portainer
```
example `users` zalecane w `group_vars/all`
```
 users:
    - name: Administrator
      username: administrator
      default_password: "aaa"
      state: present
```

Przykładowy Playbook
----------------

Przykładowy playbbok
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

Testowanie
------------

Testing on:
  - Ubuntu 16.04 LTS
  - Ubuntu 18.04 LTS
  - Ubuntu 20.04 LTS
  - Centos 7
  - Centos 8

Licencja
-------

BSD

Autor
------------------
 **Maciej Rachuna**
##### System Administrator & DevOps Engineer
rachuna.maciej@gmail.com
