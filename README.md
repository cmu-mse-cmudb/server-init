# server-init
This repo is a collection of ansible scripts for initialization of the servers for the testing infra of the [NoisePage](https://github.com/cmu-db/terrier) project

## Server grouping
The servers are grouped as followed
- `k8s-masters`: the master nodes for the kubernetes cluster
- `k8s-workers`: the worker nodes for the kubernetes cluster
  - `testing`: the servers in the testing env
  - `staging`: the servers in the staging env
  - `production`: the servers in the production env

## How to use it?
- Install ansible
  - Create your virtualenv by running `virtualenv env $(which python3)`
  - Install all the dependencies by running `pip3 install -r requirements.txt`
- Configure ansible inventory
  - Duplicate the `inventory.template` by running `cp inventory.template cp`
  - Change the `ansible_user = {YOUR SSH ACCOUNT}`
- SSH permissions
  - Make sure you have the ssh access to **all** the servers you want to init
- Execute server init
  - Run `ansible-playbook -i inventory -e env={testing|staging|production|k8s-master|k8s-worker} playbooks/init.yml` to init the servers in the respective server groups

## What it does?
Currently, it will install and configure the following items on the servers
- Linux basic tools
  - vim
  - htop
  - curl
  - net-tools
  - iptables
- Docker
  - start and enable the docker daemon
- Python3.7
  - pip
  - virtualenv