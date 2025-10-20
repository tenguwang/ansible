# 安装ansible

## 准备环境
```
wget http://fiels.tenguwang.com/ansible/ansible-2.9.9.tar.gz

apt install python-pip
```

## 安装
```
pip install ansible-2.9.9.tar.gz
```

> ansuble主控端需要安装sshpass
```
apt install -y sshpass
```

## 验证
```
root@ops:/opt/ansible# ansible --version
ansible 2.9.9
  config file = /opt/ansible/ansible.cfg
  configured module search path = [u'/opt/ansible/library']
  ansible python module location = /usr/local/lib/python2.7/dist-packages/ansible
  executable location = /usr/local/bin/ansible
  python version = 2.7.17 (default, Mar 18 2022, 13:21:42) [GCC 7.5.0]
```


# ansible初始化

## 配置主机列表

```shell
cat ./inventories/hosts
node1 ansible_host=172.16.140.131
```

- node1   主机名称(可以不存在)
- ansible_host   节点IP地址

## 修改用户信息

> 该信息用于连接各服务器进行初始化操作，需要sudo权限

```shell
cat inventories/group_vars/all 
# Connection server user information
ansible_ssh_user: 'megaium'
ansible_ssh_port: '22'
ansible_ssh_pass: 'Megaium!'
ansible_become_pass: 'Megaium!'
# ansible_ssh_private_key_file: keys/id.rsa

# Elevate privileges
ansible_become: true
```

## 初始化操作

```shell
cd /opt/ansible
ansible-playbook playbooks/sys_init.yml -b
```



