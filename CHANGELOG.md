# Change Log
All notable changes to this project will be documented in this file.

## [Unreleased](https://github.com/idealista/elasticsearch_role/tree/develop)
### Fixed
*[56](https://github.com/idealista/elasticsearch_role/issues/56)* Add notify restart when drop-in file content changed @aarapiles

## [2.1.2](https://github.com/idealista/elasticsearch_role/tree/2.1.2)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/2.1.1...2.1.2)
### Fixed
*[52](https://github.com/idealista/elasticsearch_role/issues/52) Fix jvm.options for different jvm major versions* @Pablohn26

## [2.1.1](https://github.com/idealista/elasticsearch_role/tree/2.1.1)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/2.1.0...2.1.1)
### Fixed
*[49](https://github.com/idealista/elasticsearch_role/issues/49) Notify restart after version update on deb install mode* @adrian-arapiles  
*[49](https://github.com/idealista/elasticsearch_role/issues/49) Correctly reinstall plugins after version change* @adrian-arapiles

## [2.1.0](https://github.com/idealista/elasticsearch_role/tree/2.1.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/2.0.1...2.1.0)
### Added 
*[46](https://github.com/idealista/elasticsearch_role/issues/46) Be able to use custom uid and gid on elasticsearch user and group* @adrian-arapiles

## [2.0.1](https://github.com/idealista/elasticsearch_role/tree/2.0.1)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/2.0.0...2.0.1)
### Fixed
- *[43](https://github.com/idealista/elasticsearch_role/issues/43) Change owner of `elasticsearch_data_dir` on deb installation* @adrian-arapiles

## [2.0.0](https://github.com/idealista/elasticsearch_role/tree/2.0.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.7.1...2.0.0)
### Added
- *[#33](https://github.com/idealista/elasticsearch_role/issues/33) Support for install elasticsearch as unzipped tar as previous versions for default installation mode* @adrian-arapiles
- *[#33](https://github.com/idealista/elasticsearch_role/issues/33) Support for install elasticsearch as debian service.* @adrian-arapiles
- *[#33](https://github.com/idealista/elasticsearch_role/issues/33) Support for install opendistroelasticsearch distribution.* @adrian-arapiles
### Changed
- *Update test-requirements dependencies and goss* @adrian-arapiles
- *[#28](https://github.com/idealista/elasticsearch_role/issues/28) Update default versions to current* @adrian-arapiles
- *[#29](https://github.com/idealista/elasticsearch_role/issues/29) Tests with buster distribution and java 11* @adrian-arapiles
- *Replaces all plugins installation in favor of ansible elasticsearch_plugin module* @adrian-arapiles
- *Improve the task for check if elasticsearch installed (in tar install) that avoid reinstall if node has service stopped* @adrian-arapiles

## [1.7.1](https://github.com/idealista/elasticsearch_role/tree/1.7.1)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.7.0...1.7.1)
### Added
- *[#25](https://github.com/idealista/elasticsearch_role/issues/25) Variable to overwrite log4j2.properties template* @adrian-arapiles
 
## [1.7.0](https://github.com/idealista/elasticsearch_role/tree/1.7.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.6.0...1.7.0)
### Added
- *[#22](https://github.com/idealista/elasticsearch_role/issues/22) Avoid double restart when upgrading or service was stopped* @adrian-arapiles

### Fixed
- *Fixed typo double run test on travis.yml* @adrian-arapiles

## [1.6.0](https://github.com/idealista/elasticsearch_role/tree/1.6.0)
[Full Changelog](https://github.com/idealista/elasticsearch_role/compare/1.5.0...1.6.0)
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
