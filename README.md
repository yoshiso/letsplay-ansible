## Requirements

direnv
docker-machine
ansible

## Setup

cp .envrc.sample .envrc
vi .envrc # edit environment variables
direnv allow .


## #1, Ping to target servers.

First, checkout tags/#1 branch. 

```shell
git checkout #1
```

### Start ec2 servers.

```shell
./bin/up-machine-01
./bin/up-machine-02
```

### Edit your hosts

```shell
vi hosts # edit ansibel_ssh_host
cat hosts
[ec2]
ec2-01 ansible_ssh_host=YOUR_EC2_HOST_01 ansible_ssh_private_key_file=~/.docker/machine/machines/ec2-01/id_rsa ansible_user=ubuntu
ec2-02 ansible_ssh_host=YOUR_EC2_HOST_02 ansible_ssh_private_key_file=~/.docker/machine/machines/ec2-02/id_rsa ansible_user=ubuntu
```

### Ping ec2 machine

All of ec2

```shell
ansible ec2 -m ping
```

Each instance.

```shell
ansible ec2-01 -m ping
ansible ec2-02 -m ping
```

Run command

```shell
ansible ec2 -m command -a uptime
ansible ec2 -m command -a "ls -la /"
```

## #2, Run simple playbook, deploy nginx servers to all ec2 instances.

Second, checkout tags/#2 branch

```shell
git checkout #2
```

Check diff, add web.yml and template files.

```
git diff #1 #2
```

Run web.yml playbook, and deploy nginx servers to all ec2 instances.

```
ansible-playbook web.yml
```

Check it. But before check, you should edit aws ec2 security gruop settings to access port http:80, https:443.

```
open http://$(docker-machine ip ec2-01)
open http://$(docker-machine ip ec2-02)
```

Looks good.

## #3, Refactor with using role.


```shell
git checkout #3
```

check diff

```shell
git diff #2 #3
```

Run web.yml playbook, and check nothing changed.



