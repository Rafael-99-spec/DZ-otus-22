# ДЗ №22 Сбор и анализ логов
### Домашнее задание
```
Настраиваем центральный сервер для сбора логов
в вагранте поднимаем 2 машины web и log
на web поднимаем nginx
на log настраиваем центральный лог сервер на любой системе на выбор
- journald
- rsyslog
- elk
настраиваем аудит следящий за изменением конфигов нжинкса

все критичные логи с web должны собираться и локально и удаленно
все логи с nginx должны уходить на удаленный сервер (локально только критичные)
логи аудита должны также уходить на удаленную систему
```
- Для разворачивания стенда, необходимо склониовать репозиторий на локальное хранилище - ```git clone https://github.com/Rafael-99-spec/DZ-otus-22```
- Далее зайти в папку репозитория - ```cd /DZ-otus-22```, и запустить стенд - ```vagrant up```. В качестве централизованного сервере журналирования выступает - ```rsyslog```,
а в качестве веб-сервера - ```webserver```.
- На ВМ ```webserver``` развернут nginx, и настроено журнлирование в /var/log/nginx/. А также журналирование в папку /var/log/rsyslog/%HOSTNAME% на сервере ```rsyslog```, в котором соответственно настроаена служба rsyslog.
ВНИМАНИЕ! /var/log/rsyslog/webserver/nginx.log появится после сразу после перезапуска службы или какого либо изменения конфигурационного файла - /etc/nginx/nginx.conf.
