# Project Title

We use Docker images to ensure a known base state for which to run our roles against. 

For our testing needs, a Docker image can be thought of as just another Ansible host. 

We’ll use the Ansible role ‘provision_docker’ to create the hosts. The interface to the role is much like an Ansible cloud module interface. 

A dynamic inventory group is created for the newly minted hosts that you can interact with in your playbook.

Includes a playbook that install a minecraft server for testing purposes


### Prerequisites

Docker 

ansible-galaxy install yauh.java8 (https://galaxy.ansible.com/yauh/java8/)

ansible-galaxy install provision_docker (https://github.com/chrismeyersfsu/provision_docker/tree/master/files)


```
Now’s a good time for an example:

---
- name: Bring up docker containers
  hosts: localhost
  gather_facts: false
  vars:
    inventory:
      - name: iptables_host_1
        image: "chrismeyers/centos6"
  roles:
    - { role: provision_docker, provision_docker_inventory: "{{inventory}}" }


- name: Hello world
  hosts: docker_containers
  tasks:
    - debug: msg=”Hello World”
```

### Installing

ansible-playbook  test.yml

test.yml  use an ubuntu image for create the container with name minecraft_host_1

 inventory:
      - name: minecraft_host_1
        image: "ubuntu-upstart:14.04"

Base distro Docker images don’t normally come with ssh running. Nor do they have their init systems enabled. I have used the image ubuntu-upstart:14.04 that have running ssh and the init system. Enough to ensure Ansible service module works against them and they can be sshed into 


## Running the tests

added a .gitlab-ci.yml for testing purposes


## Authors

* ** Juan Vicente Herrera ** - *Initial work* - juan.vicente.herrera@gmail.com


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

