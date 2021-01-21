# RedHat Ansible
Version for ansible 2.9.6
### 1. Install
```
yum install ansible
```

### 2. Setting you server.
file: /etc/ansible/hosts.
```
[group1]
s[1-4].axinyue.club

[group2]
vip.axinyue.club
```
group1 contains:
```
s1.axinyue.club
s2.axinyue.cub
```
* [Hosts Setting](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)


### 3. run
```
ansible group1 -a "/bin/echo hello"
```

### 4. use module

```
ansible -m shell -a "echo hello"
```
ps. 在2.10版本中对module 进行了分组管理,例如: shell module修改为了ansible.builtin.shell

* [ansible 2.9 module use](https://docs.ansible.com/ansible/2.9/user_guide/intro_adhoc.html#intro-adhoc)
* [ansible 2.9 modules](https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html)

* [latest modules](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html#plugins-in-ansible-builtin)


### 扩展
1. Ansible-console  控制台工具
2. Ansible-config  配置工具
3. Ansible-doc   文档工具
4. Ansible-inventory 库存
5. Ansible-playbook  剧本（批量任务）
6. Ansible-pull 从VCS获取剧本执行
7. nsible-vault Ansible数据文件加密解密
8. Ansible-galaxy 管理Ansible角色(插件)