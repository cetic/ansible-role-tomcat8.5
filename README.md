# Ansible Role: Tomcat v8.5

[![Build Status](https://travis-ci.org/cetic/ansible-role-tomcat8.5.svg?branch=master)](https://travis-ci.org/cetic/ansible-role-tomcat8.5)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-_cetic.tomcat-blue.svg)](https://galaxy.ansible.com/cetic/tomcat/)

Installs [Tomcat](http://tomcat.apache.org/) v8.5 on RHEL/CentOS 7 with [ansible](http://www.ansible.com/home).

The goal here is to provide a standalone tomcat role that can be added into your playbooks.

The ansible role allows you to install, for the moment, the version 8.5 of Tomcat.

## Requirements

You can use this ansible role to set up java:
* https://github.com/geerlingguy/ansible-role-java

## Role Variables for Tomcat 8.5

Available variables are listed below, along with default values (see `defaults/main.yml`):

### tomcat

	tomcat_version: '8.5.31'
	tomcat_port: '8080'
	tomcat_port_ajp: '8009'
	tomcat_port_https: '8443'
	tomcat_port_shutdown: '8005'
	tomcat_group: 'tomcat'
	tomcat_user: 'tomcat'
	tomcat_user_home: '/opt/tomcat'
	
You can set variables related to tomcat here.
	
### geerlingguy java

	java_home: '/lib/jvm/jre-1.8.0-openjdk'
	
## Dependencies

  - geerlingguy.java

## Example Playbook

```yaml
- hosts: tomcat
  become: true
  roles:
    - role: geerlingguy.java
    - role: cetic.tomcat
```

## Tests

### testing locally with [Vagrant](https://www.vagrantup.com/)

You can test this ansible role by using `vagrant`. See the Vagrantfile.

### testing with Travis

See the playbook used for Travis CI tests (tests/test.yml).

## Future improvements

*  Provide more recent/different versions of Tomcat
*  More OS support

Feel free to contribute.

## License

MIT License https://github.com/cetic/ansible-role-tomcat8.5/blob/master/LICENSE
