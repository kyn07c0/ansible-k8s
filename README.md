Этот Ansible playbook предназначен для автоматизированного развертывания Kubernetes кластера. 
Проект структурирован по ролям, где каждая роль отвечает за установку и настройку конкретного компонента Kubernetes.

## Роли компонентов кластера Kubernetes

### Компоненты Control Plane
1. etcd - распределенное key-value хранилище, используемое Kubernetes для хранения всех данных кластера.  
- устанавливает и настраивает etcd
- настраивает TLS аутентификацию
- конфигурирует systemd сервис

2. kube_apiserver - основной управляющий компонент, который предоставляет API Kubernetes
- устанавливает kube-apiserver
- настраивает авторизацию и аутентификацию
- конфигурирует TLS сертификаты
- настраивает systemd сервис

3. kube_control_manager - контроллер, который следит за состоянием кластера
- устанавливает kube-controller-manager
- настраивает подключение к API серверу
- конфигурирует systemd сервис

4. kube_scheduler - компонент, отвечающий за планирование подов на ноды
- устанавливает kube-scheduler
- настраивает подключение к API серверу
- конфигурирует systemd сервис

### Компоненты Worker Node
5. kubelet - основной агент на каждой ноде
- устанавливает kubelet
- настраивает аутентификацию с API сервером
- конфигурирует systemd сервис

6. kube_proxy - сетевой прокси, реализующий сервисы Kubernetes
- устанавливает kube-proxy
- настраивает работу в режиме iptables или ipvs
- конфигурирует systemd сервис

### Инфраструктурные компоненты
7. containerd - среда выполнения контейнеров
- устанавливает и настраивает containerd
- конфигурирует systemd сервис

8. runc - низкоуровневый рантайм для контейнеров
- устанавливает runc

9. cni - плагины Container Network Interface
- устанавливает CNI плагины
- настраивает сетевые плагины (Flannel, Calico и др.)

10. pod_route - настройка маршрутов для подов
- конфигурирует сетевые маршруты

11. crictl - CLI для работы с CRI (Container Runtime Interface)
- устанавливает crictl утилиту

12. kubectl - CLI для управления Kubernetes
- устанавливает kubectl
- настраивает конфигурационный файл

13. selfsigned_cert - генерация самоподписанных сертификатов
- создает CA и сертификаты для компонентов
- генерирует сертификаты для etcd, kube-apiserver и др.

# Требования
Ansible 2.9+  
Целевые серверы с ОС Debian (или совместимыми)  
Доступ по SSH с правами sudo  
Интернет-доступ для загрузки пакетов  

# Использование
Клонируйте репозиторий:

git clone https://github.com/kyn07c0/ansible-k8s.git
cd ansible-k8s
Отредактируйте файл инвентаризации static.yaml, указав ваши серверы:
```
all:
  children:
    admin:
      hosts:
        k8s-admin:
          ansible_host: 192.168.88.30
    master:
      hosts:
        k8s-master:
          ansible_host: 192.168.88.31
    worker:
      hosts:
        k8s-worker1:
          ansible_host: 192.168.88.32
          pod_subnet: 192.168.1.0/24
        k8s-worker2:
          ansible_host: 192.168.88.33
          pod_subnet: 192.168.2.0/24
```

Настройте переменные в group_vars/all.yml под вашу инфраструктуру.

Запустите playbook для развертывания control plane:
```
ansible-playbook -i inventory.ini site.yml --tags control_plane
```
Запустите playbook для развертывания worker nodes:
```
ansible-playbook -i inventory.ini site.yml --tags worker_nodes
```
Для развертывания всего кластера сразу:
```
ansible-playbook -i inventory.ini site.yml
```

Дополнительные теги
Вы можете запускать отдельные компоненты с помощью тегов:
--tags etcd - только etcd  
--tags control_plane - все компоненты control plane  
--tags networking - сетевые компоненты (CNI, kube-proxy)  
--tags runtime - containerd, runc, crictl  

Настройка  
Основные параметры кластера можно настроить в файлах:  
group_vars/all.yml - общие настройки для всех узлов  
group_vars/control_plane.yml - настройки для control plane  
group_vars/worker_nodes.yml - настройки для worker nodes  

Лицензия  
MIT License
