#Version 2.0.0 upgrade guide

With this version `2.0.0` we introduce several changes.

- Now you can install elasticsearch as tar.gz or as debian package.
- You can choose between `oss` version or `official` version.
- Now is possible to install `opendistro` amazon distro as deb package.
- Improve task for install plugins using module of ansible.

Next we'll show you how to migrate plugins from 1.x.x to 2.0.0.

### Plugins
In 1.x.x release, if we want to install plugins our yml seems like that:
```
---
#...another variable configuration
- name: Elasticsearch with custom configuration
  hosts: localhost
  roles:
    - role: idealista.elasticsearch_role
  vars:      
    elasticsearch_plugins:
      - plugin: ingest-geoip
    # - plugin: another_plugin_name
```

Now, in 2.x.x release, we changed to:
```
---
#... another variable configuration
- name: Elasticsearch with custom configuration
  hosts: localhost
  roles:
    - role: idealista.elasticsearch_role
  vars:      
    elasticsearch_plugins:
      - name: mapper-size
        state: present
    #    # Where binary of elasticsearch-plugin is to install plugins
    #    plugin_bin: "{{ elasticsearch_home }}/bin/elasticsearch-plugin" # Optional
    #    # Where plugins are saved
    #    plugin_dir: "{{ elasticsearch_home }}/plugins" # Optional
    #    # Version of plugin, default to elasticsearch_version
    #    version: "{{ item.version | default (elasticsearch_version) }}" # Optional
    #    # Proxy host to use during plugin installation
    #    proxy_host: "{{ item.proxy_host | default(omit) }}" # Optional
    #    # Proxy port to use during plugin installation
    #    proxy_port: "{{ item.proxy_port | default(omit) }}" # Optional
    #    # Optionally set the source location to retrieve the plugin from. This can be a file:// URL to install from a local
    #    # file, or a remote URL. If this is not set, the plugin location is just based on the name.
    #    src: "{{ item.src | default(omit) }}" # Optional
    #    # Force to install
    #    force: "{{ item.force | default(omit) }}" # Optional
    #
```
So basically, you have to change `plugin` to `name` on each dictionary in `elasticsearch_plugins` list.

The parameters `state` and `version` are optional but highly recommended being explicitly set. 
If not set, `state` has default value of `present` and `version` put the same version of elasticsearch. 

The rest of parameters is optional too and give you extended options to download plugins.

More documentation about these parameters can be found on [module ansible documentation](https://docs.ansible.com/ansible/2.8/modules/elasticsearch_plugin_module.html#elasticsearch-plugin-module).
