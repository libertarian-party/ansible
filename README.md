Конфигурация Ansible
====================

Конфигурация верхнего уровня для развёртывания инфраструктуры базы данных
Либертарианской партии России с помощью [Ansible](https://www.ansible.com).



Содержание
----------

* [Обзор](#конфигурация-ansible)
* [Содержание](#содержание)
* [Подготовка](#подготовка)
* [Использование](#использование)



Подготовка
----------

Конфигурация зависит от ролей Ansible, указанных в файле `requirements.yml`.
Следующую команду нужно запускать перед началом работы с конфигурацией,
а также после добавления ролей или изменения их версий:

```
ansible-galaxy install -r requirements.yml -f
```



Использование
-------------

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
