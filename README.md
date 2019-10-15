Конфигурация Ansible
====================

Конфигурация верхнего уровня для развёртывания инфраструктуры базы данных
Либертарианской партии России с помощью [Ansible](https://www.ansible.com).



Содержание
----------

* [Обзор](#конфигурация-ansible)
* [Содержание](#содержание)
* [Именование серверов](#именование-серверов)
* [Подготовка конфигурации](#подготовка-конфигурации)
* [Использование конфигурации](#использование-конфигурации)



Именование серверов
-------------------

Идентификация серверов производится с помощью `A` и `AAAA` записей DNS.
В качестве имён используются английские наименования греческих букв, например:

* `alpha.libertarian-party.com`
* `beta.libertarian-party.com`
* `gamma.libertarian-party.com`
* `delta.libertarian-party.com`

Для именования логических доменных имён используются `CNAME` записи DNS,
которые указывают на один из идентификаторов серверов:

* `libertarian-party.com` -> `alpha.libertarian-party.com`
* `www.libertarian-party.com` -> `alpha.libertarian-party.com`
* `stg.libertarian-party.com` -> `delta.libertarian-party.com`



Подготовка конфигурации
-----------------------

Для ускорения работы Ansible используется библиотека
[Mitogen](https://mitogen.networkgenomics.com/). Необходимо установить её
в директорию `vendor`:

```
wget -O vendor/mitogen-0.2.8.tar.gz https://networkgenomics.com/try/mitogen-0.2.8.tar.gz
tar -xzf vendor/mitogen-0.2.8.tar.gz -C vendor/
```

Конфигурация зависит от ролей [Ansible Galaxy](https://galaxy.ansible.com),
указанных в файле `requirements.yml`. Следующую команду нужно запускать
перед началом работы с конфигурацией, а также после добавления ролей
или изменения их версий:

```
ansible-galaxy install -r requirements.yml -f
```



Использование конфигурации
--------------------------

Перезагрузка всех серверов:

```
ansible all -m reboot
```

Обновление системных пакетов на всех серверах:

```
ansible all -m apt -a 'update_cache=yes upgrade=yes'
```

Развёртывание всей инфраструктуры:

```
ansible-playbook playbooks/site.yml
```
