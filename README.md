# Ansible Kibana
[![Build Status](https://travis-ci.org/supertarto/ansible-kibana.svg?branch=master)](https://travis-ci.org/supertarto/ansible-kibana)

Install and configure Kibana with Ansible. It's meant to be used with elasticsearch (supertarto.elasticsearch role on Galaxy). For Debian only, the installation use the elasticsearch repository.

## Requirements
None, but can be used with Elasticsearch.

## Tested plateform
* Debian 10 (Buster)

## Role variables
Kibana version, and informations used during the installation.
```yml
kibana_version: "7.4.1"
kibana_repo_base: "https://artifacts.elastic.co"
kibana_apt_key: "{{ kibana_repo_base }}/GPG-KEY-elasticsearch"
kibana_apt_key_id: "46095ACC8548582C1A2699A9D27D666CD88E42B4"
kibana_apt_url: "deb {{ kibana_repo_base }}/packages/{{ kibana_major_version }}/apt stable main"
kibana_package_name: "kibana"
```
Set to True if you want to set the package on hold, to prevent unwanted upgrade.
```yml
kibana_version_lock: false
```
The kibana group and some important directories path. By default, **kibana_pid_dir** is not set.
```yml
kibana_group: root

kibana_conf_dir: "/etc/kibana"
# kibana_pid_dir: "/var/run"
```
Variables used in kibana.yml. By default, **kibana_elasticsearch_username** and **kibana_elasticsearch_password** are not set.
```yml
kibana_server_host: "localhost"
kibana_server_port: 5601
kibana_elasticsearch_url: "http://localhost:9200"
kibana_elasticsearch_preserve_host: true
kibana_index_name: ".kibana"
kibana_default_app_id: "discover"
# kibana_elasticsearch_username: []
# kibana_elasticsearch_password: []
kibana_logging_dest: "stdout"
kibana_logging_silent: false
kibana_logging_quiet: false
kibana_logging_verbose: false
```
## Examples
```yml
- hosts: somehost
  roles:
    - supertarto.kibana
  vars:
    kibana_server_host: "localhost"
    kibana_server_port: 5601
    kibana_elasticsearch_url: "http://localhost:9200"
```

## Installation
```
ansible-galaxy install supertarto.kibana
```
## License
GPL V3.0
