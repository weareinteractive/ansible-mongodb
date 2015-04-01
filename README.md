# Ansible MongoDB Role

[![Build Status](https://travis-ci.org/weareinteractive/ansible-mongodb.png?branch=master)](https://travis-ci.org/weareinteractive/ansible-mongodb)
[![Stories in Ready](https://badge.waffle.io/weareinteractive/ansible-mongodb.svg?label=ready&title=Ready)](http://waffle.io/weareinteractive/ansible-mongodb)

> `mongodb` is an [ansible](http://www.ansible.com) role which:
>
> * installs mongodb
> * configures mongodb

## Installation

Using `ansible-galaxy`:

```
$ ansible-galaxy install franklinkim.mongodb
```

Using `requirements.yml`:

```
- src: franklinkim.mongodb
```

Using `git`:

```
$ git clone https://github.com/weareinteractive/ansible-mongodb.git roles/franklinkim.mongodb
```

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```
# mongodb_package: mongodb-org=3.0.1

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

# start on boot
mongodb_service_enabled: yes
# current state: started, stopped
mongodb_service_state: started
```

## Example playbook

```
- hosts: all
  suod: yes
  roles:
    - franklinkim.mongodb
  vars:
    mongodb_packages:
      - mongodb-org=3.0.1
```

## Testing

```
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

## License
Copyright (c) We Are Interactive under the MIT license.
