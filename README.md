## Kubernetes Ansible Vagrant

**If you want to run a kubernetes cluster for studying purposes this project is for you.**

**There is no need to use a cloud provider you can spawn your own cluster in your machine**

**Minimum hardware requirements:**

- 2GB for each node besides the minimum requirements for your own operating system
- 2 CPUs

This project uses virtualbox as its provider.

https://www.virtualbox.org/wiki/Downloads

Install vagrant.

https://developer.hashicorp.com/vagrant/downloads

This project uses ansible so its necessary to have at least python 3 up and running

```shell
pip install requirements.txt
```

then just 

```shell
vagrant up
```