# Ansible-Docker

Ansible + Docker
Playground for doing Docker things with Ansible. Currently demoing a single method of building Docker images using Ansible.

## How to use
#### Vagrant
The included Vagrantfile ensures a standard host environment with ansible and docker.

```shell
username@localhost:~$ vagrant up
username@localhost:~$ vagrant ssh
vagrant@vagrant:~$ sudo ansible-playbook -i localhost, /src/ansible/playbook.yml
```

#### Linux (local)
On OSX requires a host VM however if you are developing on Linux with docker and ansible installed locally you can

```shell

$ sudo ansible-playbook -i localhost, docker-image-build.yml
```

## Ansible, building Docker images with
The included playbook docker-image-build.yml, demonstrates how to use ansible via ansible_connection=docker and `docker commit` to build images from ansible roles rather than `Dockerfile`.
### How to use

#### Vagrant
```shell
$ vagrant up
```

#### Linux (local)
```shell
$ sudo ansible-playbook -i localhost, playbook.yml
```

### TODO:

* Push images to remote repository
 * (awaiting ansible 2.2 update to docker_image push)
 * can be done now using ansible:
 ```ansible
  command: docker push myRegistry.com/myImage:myTag
 ```

* Ensure ability to connect to remote docker_host securely.
http://docs.ansible.com/ansible-container/installation.html#securing-docker-daemon-with-tls

* (low prority) Add a Dockerfile anyway (*gasp!*} which ensures python on the FROM image somehow depending on base...
