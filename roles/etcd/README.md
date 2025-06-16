Роль etcd
=========

Эта Ansible роль автоматизирует развёртывание и настройку etcd кластера.

Требования
------------

Требования к роли описаны в основном README.md файле.

Переменные роли
--------------

Роль имеет следующие переменные:  

| Переменная             | Описание                                                  | Значение по умолчанию |
|------------------------|-----------------------------------------------------------|-----------------------|
| etcd_version           | Версия etcd для установки.                                | 3.5.19                |
| etcd_extract_dir       | Директория для извлечения архива etci.                    | /opt                  |
| etcd_binary_dir        | Директория для размещения бинарных файлов etcd.           | /usr/local/bin        |
| etcd_data_dir          | Директория для хранения данных etcd.                      | /var/lib/etcd         |
| etcd_install_mode      | Режим загрузки архива etcd (network, local).              | network               |
| etcd_local_binary_dir  | Расположение архива etcd для режима загрузки local.       | /home/yura/k8s/binary |
| etcd_ips               | Список ip адресов кластера etcd (вычисляемое значение)    |                       |
| etcd_dns_names         | Список доменных имён кластера etcd (вычисляемое значение) |                       |
| etcd_protocol          | Протокол работы кластера etcd                             | "https"               |
| etcd_client_port       | Порт для клиентских запросов                              | 2379                  |
| etcd_peer_port         | Порт для peer-запросов                                    | 2380                  |


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
