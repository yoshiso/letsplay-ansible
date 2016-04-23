## Requirements

direnv
docker-machine
ansible

## Setup

cp .envrc.sample .envrc
vi .envrc # edit environment variables
direnv allow .


## #1, Ping to target servers.

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
