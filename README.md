![Logo](https://raw.githubusercontent.com/idealista/elasticsearch_role/master/logo.gif)

[![Build Status](https://travis-ci.org/idealista/elasticsearch_role.png)](https://travis-ci.org/idealista/elasticsearch_role)

# Elasticsearch Ansible role

- [Getting Started](#getting-started)
  - [Prerequisities](#prerequisities)
  - [Installing](#installing)
- [Usage](#usage)
- [Testing](#testing)
- [Built With](#built-with)
- [Versioning](#versioning)
- [Authors](#authors)
- [License](#license)
- [Contributing](#contributing)

## Getting Started

**THIS ROLE IS FOR 6.x or 7.x**

Ansible role for 6.x/7.x Elasticsearch. Currently this works on Debian based linux systems. Tested platforms are:

* Debian 8
* Debian 9

These instructions will get you a copy of the role for your ansible playbook. Once launched, it will install a [Elasticsearch](https://www.elastic.co/products/elasticsearch) distributed, RESTful search and analytics engine in a Debian system.

### Prerequisities

#### To execute this role:

Ansible 2.8.8 version installed.

#### For testing purposes:

* Python 3.6
* [Molecule](https://molecule.readthedocs.io/)
* [Pipenv](https://github.com/pypa/pipenv) 
* [jmespath](http://jmespath.org/) 
* [Docker](https://www.docker.com/) as driver


### Installing

Create or add to your roles dependency file (e.g requirements.yml):

```yml
- src: http://github.com/idealista/elasticsearch_role.git
  scm: git
  version: 1.7.1
  name: elasticsearch
```

Install the role with ansible-galaxy command:

```sh
ansible-galaxy install -p roles -r requirements.yml -f
```

Use in a playbook:

```yml
- hosts: someserver
  roles:
    - role: elasticsearch
```

## Usage

Look to the [defaults](defaults/main.yml) properties file to see the possible configuration properties.

All Elasticsearch configuration parameters are supported. This is achieved using a configuration map parameter 'elasticsearch_config' which is serialized into the elasticsearch.yml file.
The use of a map ensures the Ansible playbook does not need to be updated to reflect new/deprecated/plugin configuration parameters.

In addition to the elasticsearch_config map, several other parameters are supported for additional functions e.g. script installation. These can be found in the role's defaults/main.yml file.

## Elastic 6.x
The following illustrates applying configuration parameters to an Elasticsearch 6.x instance.

```yaml
- name: Elasticsearch with custom configuration
  hosts: localhost
  roles:
    - role: idealista.elasticsearch_role
  vars:      
    elasticsearch_version: 6.8.6
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      node.name: node1
      http.port: 9200
      transport.tcp.port: 9300
      node.data: true
      node.master: true
      bootstrap.memory_lock: true
    elasticsearch_heap_size: 1g
    elasticsearch_api_host: localhost
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip
```

See https://www.elastic.co/guide/en/elasticsearch/reference/current/settings.html for further details on available options.


#### Important Note

**The role uses elasticsearch_api_host and elasticsearch_api_port to communicate with the node for actions only achievable via http e.g. to install templates and to check the NODE IS ACTIVE.  These default to "localhost" and 9200 respectively.  
If the node is deployed to bind on either a different host or port, these must be changed.**


### Multi Node Server Installations

The application of the elasticsearch role results in the installation of a node on a host. Specifying the role multiple times for a host therefore results in the installation of multiple nodes for the host. 

An example of a three server deployment is shown below. The three servers work as master and data nodes.


```yaml
  hosts: node1
  roles:
    - role: idealista.elasticsearch_role
  vars:
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      elasticsearch_version: 6.8.6
      node.name: node1
      cluster.name: idealista-cluster
      discovery.zen.ping.unicast.hosts: ["node1", "node2", "node3"]
      discovery.zen.minimum_master_nodes: 2
      network.host: _site_
      http.port: 9200
      transport.tcp.port: 9300
      node.master: true
      node.data: true
      bootstrap.memory_lock: true
    elasticsearch_api_host: node1
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip

- hosts: node2
  roles:
    - role: idealista.elasticsearch_role
  vars:
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      elasticsearch_version: 6.8.6
      node.name: node2
      cluster.name: idealista-cluster
      discovery.zen.ping.unicast.hosts: ["node1", "node2", "node3"]
      discovery.zen.minimum_master_nodes: 2
      network.host: _site_
      http.port: 9200
      transport.tcp.port: 9300
      node.master: true
      node.data: true
      bootstrap.memory_lock: true
    elasticsearch_api_host: node2
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip
    
- hosts: node3
  roles:
    - role: idealista.elasticsearch_role
  vars:
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      elasticsearch_version: 6.8.6
      node.name: node3
      cluster.name: idealista-cluster
      discovery.zen.ping.unicast.hosts: ["node1", "node2", "node3"]
      discovery.zen.minimum_master_nodes: 2
      network.host: _site_
      http.port: 9200
      transport.tcp.port: 9300
      node.master: true
      node.data: true
      bootstrap.memory_lock: true
    elasticsearch_api_host: node3
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip
```
## Elastic 7.x
The following illustrates applying configuration parameters to an Elasticsearch oss (**open source without x-pack**) 
7.x instance with single-node (development).

```yaml
- name: Elasticsearch with custom configuration
  hosts: localhost
  roles:
    - role: idealista.elasticsearch_role
  vars:
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      node.name: node1
      discovery.type: single-node
      node.data: true
      node.master: true
      bootstrap.memory_lock: true
    elasticsearch_heap_size: 1g
    elasticsearch_api_host: localhost
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip
```

See https://www.elastic.co/guide/en/elasticsearch/reference/current/settings.html for further details on available options.


#### Important Note

**The role uses elasticsearch_api_host and elasticsearch_api_port to communicate with the node for actions only achievable via http e.g. to install templates and to check the NODE IS ACTIVE.  These default to "localhost" and 9200 respectively.  
If the node is deployed to bind on either a different host or port, these must be changed.**


### Multi Node Server Installations

The application of the elasticsearch role results in the installation of a node on a host. Specifying the role multiple times for a host therefore results in the installation of multiple nodes for the host. 

An example of a three server deployment is shown below. The three servers work as master and data nodes.


```yaml
  hosts: node1
  roles:
    - role: idealista.elasticsearch_role
  vars:
    elasticsearch_version: 7.0.0
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      node.name: node1
      cluster.name: idealista-cluster
      discovery.seed_hosts: ["node1", "node2", "node3"]
      cluster.initial_master_nodes: ["node1", "node2", "node3"]
      network.host: _site_
      http.port: 9200
      transport.tcp.port: 9300
      node.master: true
      node.data: true
      bootstrap.memory_lock: true
    elasticsearch_api_host: node1
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip

- hosts: node2
  roles:
    - role: idealista.elasticsearch_role
  vars:
    elasticsearch_version: 7.0.0
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      node.name: node2
      cluster.name: idealista-cluster
      discovery.seed_hosts: ["node1", "node2", "node3"]
      cluster.initial_master_nodes: ["node1", "node2", "node3"]
      network.host: _site_
      http.port: 9200
      transport.tcp.port: 9300
      node.master: true
      node.data: true
      bootstrap.memory_lock: true
    elasticsearch_api_host: node2
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip
    
- hosts: node3
  roles:
    - role: idealista.elasticsearch_role
  vars:
    elasticsearch_version: 7.0.0
    elasticsearch_data_dir: /var/lib/elasticsearch
    elasticsearch_log_dir: /var/log/elasticsearch
    elasticsearch_config:
      node.name: node3
      cluster.name: idealista-cluster
      discovery.seed_hosts: ["node1", "node2", "node3"]
      cluster.initial_master_nodes: ["node1", "node2", "node3"]
      network.host: _site_
      http.port: 9200
      transport.tcp.port: 9300
      node.master: true
      node.data: true
      bootstrap.memory_lock: true
    elasticsearch_api_host: node3
    elasticsearch_api_port: 9200
    elasticsearch_plugins:
      - plugin: ingest-geoip
```

## Testing

```sh
pipenv shell
pipenv sync
molecule test
```
Note: Its necesary to execute this command in each container before elastic reboots: sysctl -w vm.max_map_count=262144
## Built With

![Ansible](https://img.shields.io/badge/ansible-2.8.8-green.svg)

## Versioning

For the versions available, see the [tags on this repository](https://github.com/idealista/elasticsearch_role/tags).

Additionaly you can see what change in each version in the [CHANGELOG.md](CHANGELOG.md) file.

## Authors

- **Idealista** - *Work with* - [idealista](https://github.com/idealista)

See also the list of [contributors](https://github.com/idealista/elasticsearch_role/contributors) who participated in this project.

## License

![Apache 2.0 License](https://img.shields.io/hexpm/l/plug.svg)

This project is licensed under the [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) license - see the [LICENSE](LICENSE) file for details.

## Contributing

Please read [CONTRIBUTING.md](.github/CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.
