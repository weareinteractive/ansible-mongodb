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

* Ansible >= 1.9

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---

# APT key id
mongodb_apt_key_id: EA312927
# APT key server
mongodb_apt_key_server: keyserver.ubuntu.com
# APT repository
mongodb_apt_repository: "deb http://repo.mongodb.org/apt/{{ ansible_distribution }} {{ ansible_distribution_release }}/mongodb-org/3.2 {{ 'main' if ansible_distribution == 'debian' else 'multiverse' }}"
# User
mongodb_user: mongodb
# Package
mongodb_package: mongodb-org

# Run with security
mongodb_conf_auth: no
# Directory for datafiles
mongodb_conf_dbpath: /var/lib/mongodb
# Log file to send write to instead of stdout
mongodb_conf_logpath: /var/log/mongodb/mongod.log
# Specify port number
mongodb_conf_port: 27017
# Comma separated list of ip addresses to listen on
mongodb_conf_bind_ip: 127.0.0.1
# Enable journaling
mongodb_conf_journal: no
# Append to logpath instead of over-writing
mongodb_conf_logappend: yes
# Limits each database to a certain number of files
mongodb_conf_quota: no
# Disable scripting engine
mongodb_conf_noscripting: no
# Do not allow table scans
mongodb_conf_notablescan: no
# Periodically show cpu and iowait utilization
mongodb_conf_cpu: no
# Enable http interface
mongodb_conf_httpinterface: no
# Inspect all client data for validity on receipt
mongodb_conf_objcheck: no
# Disable data file preallocation.
mongodb_conf_noprealloc: no

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
  sudo: yes
  roles:
    - franklinkim.mongodb
  vars:
    mongodb_package: mongodb-org=3.2.0

```

## Testing

```shell
$ git clone https://github.com/weareinteractive/ansible-mongodb.git
$ cd ansible-mongodb
$ vagrant up
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

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
