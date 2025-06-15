Роль etcd
=========

Эта Ansible роль автоматизирует развёртывание и настройку etcd кластера.

Требования
------------

Требования к роли описаны в основном README.md файле.

Переменные роли
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.
Роль имеет следующие переменные:  
| Переменная | Описание | Значение по умолчанию |
|---|---|---|
| etcd_version           | | 3.5.19 |
| etcd_extract_dir       | | /opt   |
| etcd_binary_dir        | | /usr/local/bin |
| etcd_data_dir          | | /var/lib/etcd |
| etcd_install_mode      | | network |
| etcd_local_binary_dir  | | /home/yura/k8s/binary |

Зависимости
------------

Эта роль не имеет прямых зависимостей от других Ansible ролей.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
