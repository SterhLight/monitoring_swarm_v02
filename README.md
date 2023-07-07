# МОНИТОРИНГ СТЕКА СЕРВЕРОВ НА SWARM
[![GitHub-Actions-lint](https://github.com/SterhLight/monitoring_swarm_v02/actions/workflows/blank.yml/badge.svg)](https://github.com/SterhLight/monitoring_swarm_v02/actions/workflows/blank.yml)
[![scheme.jpg](https://i.postimg.cc/c1zwkYVH/scheme.jpg)](https://postimg.cc/V5jJdSsQ)
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
### ПРИМЕЧАНИЕ
Подразумевается, что у администратора уже развернут стэк серверов под управлением Docker Swarm.
Пользователь от имени которого на этих серверах работает Ansible обладает на них правами администратора.
После запуска каждой из команд ниже будет предоставлен запрос на ввод пароля администратора серверов.
### Запуск проекта
```
ansible-playbook all.yml -t deploy -K
```
Чтобы перезапустить какой-либо один из сервисов применяется команда:
```
ansible-playbook all.yml -t <service1>,<service2> -K
```
где `<service>` - тот/те сервис что перезапускается
## BACKUP/RECOVERY
### Backup volums
Чтобы забэкапить созданные на управляемом сервере volums и тем самым сохранить сделаные изменения даже после потери сервера, запускается команда:
```
ansible-playbook all.yml -t backup -K
```
Все volums на управляемом сервере быдут заархивированны и полученный архив скопирован в определенное администратором место, задать которое можно в `group_vars/all/vars.yml` через переменную "backup_dst_folder", в папку с датой бэкапирования.
### Recovery volums
Чтобы восстановить volums из бэкапа выполняется команда.
```
ansible-playbook all.yml -t recovery -e bp_folder="<your-folders>" -K
```
где `<your-folders>` - папка с бэкапом с названием по времени создания бэкапа, например "2023-07-07-10:41:40"
### Удаление папок
При необходимости удалить все папки, созданные для сервисов, выполняется команда:
```
ansible-playbook all.yml -t del_folder -K
```
Но надо помнить, что в данных папках хранятся файлы конфигураций.
