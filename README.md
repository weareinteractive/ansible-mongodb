# Ansible franklinkim.mongodb role

[![Build Status](https://img.shields.io/travis/weareinteractive/ansible-mongodb.svg)](https://travis-ci.org/weareinteractive/ansible-mongodb)
[![Galaxy](http://img.shields.io/badge/galaxy-franklinkim.sudo-blue.svg)](https://galaxy.ansible.com/list#/roles/3277)
[![GitHub tag](https://img.shields.io/github/tag/weareinteractive/ansible-mongodb.svg)](https://github.com/weareinteractive/ansible-mongodb/releases)
[![GitHub stars](https://img.shields.io/github/stars/weareinteractive/ansible-mongodb.svg?style=social&label=Star)](https://github.com/weareinteractive/ansible-mongodb)

> `franklinkim.mongodb` is an [Ansible](http://www.ansible.com) role which:
>
> * installs mongodb
> * configures mongodb
> * configures logrotate

## Installation

Using `ansible-galaxy`:

```shell
$ ansible-galaxy install franklinkim.mongodb
```

Using `requirements.yml`:

```yaml
- src: franklinkim.mongodb
```

Using `git`:

```shell
$ git clone https://github.com/weareinteractive/ansible-mongodb.git franklinkim.mongodb
```

## Dependencies

* Ansible >= 2.4

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---

# Mongodb version
mongodb_version: 3.6
# APT key id
mongodb_apt_key_id: 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
# APT key server
mongodb_apt_key_server: keyserver.ubuntu.com
# APT repository
mongodb_apt_repository: "deb http://repo.mongodb.org/apt/{{ ansible_distribution|lower }} {{ ansible_distribution_release }}/mongodb-org/{{ mongodb_version }} {{ 'main' if ansible_distribution == 'debian' else 'multiverse' }}"
# User
mongodb_user: mongodb
# Package
mongodb_package: mongodb-org
# For documentation of all options, see:
# http://docs.mongodb.org/manual/reference/configuration-options/
mongodb_conf_defaults:
  systemLog:
    destination: file
    logAppend: true
    path: /var/log/mongodb/mongod.log
  storage:
    dbPath: /var/lib/mongo
    journal:
      enabled: true
  processManagement:
    fork: true
    pidFilePath: /var/run/mongodb/mongod.pid
    timeZoneInfo: /usr/share/zoneinfo
  net:
    port: 27017
    bindIp: 127.0.0.1
mongodb_conf: "{{ mongodb_conf_defaults | combine({}, recursive=True) }}"
# start on boot
mongodb_service_enabled: yes
# current state: started, stopped
mongodb_service_state: started


```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

```yaml
---

- name: reload mongodb
  service: name=mongod state=reloaded
  when: mongodb_service_state != 'stopped'

- name: restart mongodb
  service: name=mongod state=restarted
  when: mongodb_service_state != 'stopped'

```


## Usage

This is an example playbook:

```yaml
---

- hosts: all
  roles:
    - franklinkim.mongodb
  vars:
    mongodb_conf: "{{ mongodb_conf_defaults | combine({'net':{'bindIp':'0.0.0.0'}}, recursive=True) }}"

```


## Testing

```shell
$ git clone https://github.com/weareinteractive/ansible-mongodb.git
$ cd ansible-mongodb
$ make test
```

## Contributing
In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

*Note: To update the `README.md` file please install and run `ansible-role`:*

```shell
$ gem install ansible-role
$ ansible-role docgen
```

## License
Copyright (c) We Are Interactive under the MIT license.
