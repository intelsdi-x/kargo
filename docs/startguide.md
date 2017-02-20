# How to prepare development environment and run Kargo

A quick presentation how to install and use ansible in Kargo for the first time. System on which these steps were done is 16.04 Ubuntu Unity 7. For another systems and advices how to start using kargo into it, see also [ansible intro installation guide](http://docs.ansible.com/ansible/intro_installation.html).

#### Instruction how to deploy Kargo on Bare Metal

First you must install git for clone Kargo repository on your machine.

```sh
sudo apt-get install git
```

Then you can clone Kargo repository, which provide environment to run ansible. The best way is create a personal workspace where all repos (including kargo repository) will be stored. In this case it will be ~/Repos directory.

```sh
mkdir ~/Repos && cd ~/Repos
clone https://github.com/kubernetes-incubator/kargo.git
```

#### Installing all useful and necessary dependencies

 Firstly make sure that servers have access to the Internet. It is elementary step to do another commands (for instance, when you have to pull docker images).

 Secondly install ansible in v2.2 version or newer.

```sh
sudo apt-add-repository ppa:ansible/ansible -y
sudo apt-get update && sudo apt-get install ansible -y
```

Thirdly install python package.

```sh
sudo apt-get install python-netaddr
```


#### How to build inventory on your own

See [inventory example](https://github.com/kubernetes-incubator/kargo/blob/master/inventory/inventory.example).

#### Information about cluster.yml file

Here you can change k8s version, DNS information and boostrap_os.

#### Run ansible

For useful flags and limits, which help you with large deployment see [this page](https://github.com/kubernetes-incubator/kargo/blob/master/docs/large-deployments.md).

```sh
ansible-playbook -u ubuntu -b --become-user=root -i /kargo/inventory/inventory.example /kargo/cluster.yml -e kube_network_plugin=flannel -e docker_version=1.12
```

