# МОНИТОРИНГ СТЕКА СЕРВЕРОВ НА SWARM
[![GitHub-Actions-lint](https://github.com/SterhLight/monitoring_swarm_v02/actions/workflows/blank.yml/badge.svg)](https://github.com/SterhLight/monitoring_swarm_v02/actions/workflows/blank.yml)
## ЗАПУСК
### Редактирование файла инвенторизации
Требуется заменить в inventory.yml IP-адреса на актуальные
### Редактирование конфигурационного файла Ansible
При необходимости внести изменения в файл ansible.cfg.
### Требуется заменить в group_vars/all/vars.yml нижеуказанные данные на актуальные
```
advertise_addr        : 10.10.10.101
ansible_user          : user
```
### Запуск проекта
```
ansible-playbook all.yml -K
```
