ansible_ipython_machinelearning_bootstrap_conda
====

## Overview

Setup machinelearning development environment with ipython on ubuntu(ec2)
Using miniconda

ansible-playbook of [this page](http://qiita.com/icoxfog418/items/950b8af9100b64c0d8f9)

## Environment

* target server
  * OS: Ubuntu 14.04
  * Instance type: t2.micro

## Installation

See http://docs.ansible.com/intro_installation.html

## Usage

### SSH setting on local client

1. edit ~/.ssh/config to ssh target server

```
$ vim ~/.ssh/config
```

```text:~/.ssh/config
Host ec2_bootstrap
  HostName ec2-XXX-XXX-XXX-XXX.ap-northeast-1.compute.amazonaws.com
  User ubuntu
  IdentityFile ~/.ssh/hoge.pem
```

### Run playbook from local client

1. run playbook on local client

```
$ ansible-playbook tasks/main.yml
```

### Run ipython notebook server on target server(EC2)

1. ssh to target server(EC2)
2. apply conda env
3. run server

```
$ ssh ec2_bootstrap

ubuntu@ip-xxx-xxx-xxx-xxx:~$ cd scikit-learn-notebook 
ubuntu@ip-xxx-xxx-xxx-xxx:~/scikit-learn-notebook$ . /home/ubuntu/.pyenv/versions/minicondax-x.x.x/envs/ml_env/bin/activate ml_env
(ml_env)ubuntu@ip-xxx-xxx-xxx-xxx:~/scikit-learn-notebook$ ipython notebook --profile=nbserver
```

Open browser and access `http://ec2-XXX-XXX-XXX-XXX.ap-northeast-1.compute.amazonaws.com:8888/` .
## Running results

Running result summary
Using Ansible plugin [ansible-profile](https://github.com/jlafon/ansible-profile)

```
PLAY RECAP ********************************************************************
conda create ---------------------------------------------------------- 123.30s
install pyenv's python and rehash -------------------------------------- 48.80s
apt-get upgrade a server ----------------------------------------------- 30.07s
apt-get install basic pkg ---------------------------------------------- 20.81s
apt-get updates a server ----------------------------------------------- 10.42s
updating ipython configuration ----------------------------------------- 10.41s
git clone pyenv --------------------------------------------------------- 8.39s
checking notebooks port ------------------------------------------------- 8.31s
git clone scikit-learn-notebook ----------------------------------------- 6.84s
info -------------------------------------------------------------------- 6.56s
techcircle5a               : ok=19   changed=11   unreachable=0    failed=0
```

## References

* http://qiita.com/icoxfog417/items/950b8af9100b64c0d8f9
* http://docs.ansible.com/
* https://github.com/jlafon/ansible-profile
* http://supportex.net/blog/2014/10/ansible-installing-pyenv-centos/
* http://qiita.com/FGtatsuro/items/2366c93131c47aef8dfe

## Lisence

This software is released under the MIT License, see LICENSE.

