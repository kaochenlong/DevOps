# DevOps practice

## 工具

- [Vagrant](https://www.vagrantup.com) to build local virtual machine
- [Ansible](https://www.ansible.com) to complete
- [Capistrano](https://capistranorb.com) to deploy application

## 流程

Step 1. 新增主機（需安裝 [VirtualBox](https://www.virtualbox.org)）：

    $ vagrant up

Step 2. 環境設定及軟體安裝（以本機安裝為例）：

    $ ansible-playbook local_ubuntu_18.yml

by eddie@5xruby.tw
