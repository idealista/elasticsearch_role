# Change Log
All notable changes to this project will be documented in this file.

## [Unreleased](https://github.com/idealista/elasticsearch_role/tree/develop)

### Added
- *[#19](https://github.com/idealista/elasticsearch_role/issues/19) Add daemon_reload: yes to elasticsearch restart handler* @adrian-arapiles
- *Add optional drop-in template for configure elasticsearch service* @adrian-arapiles

## [1.5.0](https://github.com/idealista/elasticsearch_role/tree/1.5.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.4.0...1.5.0)
### Added
- *Added operating system configurations* @frantsao
- *Updated ElasticSearch default version* @frantsao

## [1.4.0](https://github.com/idealista/elasticsearch_role/tree/1.4.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.3.1...1.4.0)
### Added
- *[#10](https://github.com/idealista/elasticsearch_role/issues/10) Add system:true on create elasticsearch_user to get UID and GID on system range* @adrian-arapiles
- *Add goss test to check elasticsearch_user UID and GID are on system range* @adrian-arapiles
- *Update requirements* @adrian-arapiles

## [1.3.1](https://github.com/idealista/elasticsearch_role/tree/1.3.1)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.3.0...1.3.1)
### Fixed
- *Fix pid directory creation error in start* @acuervof

## [1.3.0](https://github.com/idealista/elasticsearch_role/tree/1.3.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.2.0...1.3.0)
### Changed
- *Change deprecated log format on log4j2.properties* @adrian-arapiles
- *Optimize molecule test with playbook 3 nodes at same time* @adrian-arapiles

## [1.2.0](https://github.com/idealista/elasticsearch_role/tree/1.2.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.1.0...1.2.0)
### Fixed
- *Error installing elasticsearch version 7 without elasticsearch_build_name param* @acuervof

## [1.1.0](https://github.com/idealista/elasticsearch_role/tree/1.1.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.0.0...1.1.0)
### Added
- *Add support for elastic 7 and oss versions and molecule scenario test* @adrian-arapiles
### Changed
- _Expose variable **elasticsearch_build_name** for override version to install._ @adrian-arapiles

## [1.0.0](https://github.com/idealista/elasticsearch_role/tree/1.0.0)
### Added
- *First release* @acuervof
