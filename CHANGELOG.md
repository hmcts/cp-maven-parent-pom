# Change Log
All notable changes to this project will be documented in this file, which follows the guidelines
on [Keep a CHANGELOG](http://keepachangelog.com/). This project adheres to
[Semantic Versioning](http://semver.org/).

## [Unreleased]
## [8.0.0-M1] - 2020-12-09
- Java 11 Upgrade
    - plugins.maven-plugin-plugin.version 3.6
    - plugins.maven.compiler.version 3.8.0
    - plugins.versions.version 2.5
    - plugins.maven.surefire.version 2.22.2
    - plugins.maven.failsafe.version 2.22.2
    - plugins.jacoco.version 0.8.4
    - `--illegal-access=permit` for maven-surefire-plugin


## [2.0.0] - 2020-11-02
### Changed
- Updated parent maven-super-pom to version 2.0.0
- Moved to new Cloudsmith.io repository for hosting maven artifacts
- Reverted the version updates made in 1.8.0 release (which was never used)

## [1.8.0] - 2018-11-02
_NB the following release was never used and is reverted in the 2.0.0 release_
### Changed
- Maven Plugin Version updates:
  maven-assembly-version: 3.0.0 -> 3.1.0
  maven-clean-plugin: 3.0.0 -> 3.1.0
  maven-compiler-version: 3.6.1 -> 3.8.0
  maven-dependency-version: 3.0.1 -> 3.1.1
  maven-jar-version: 3.0.2 -> 3.1.0
  maven-javadoc-version: 2.10.4 -> 3.0.1
  maven-plugin-plugin-version: 3.5 -> 3.6.0
  maven-processor-version: 3.3.1 -> 3.3.3
  maven-resources-version: 3.0.2 -> 3.1.0
  maven-shade-version: 3.0.0 -> 3.2.0
  maven-site-version: 3.6 -> 3.7.1
  maven-surefire-version: 2.20 -> 2.22.1
  maven-wagon-version: 2.10 -> 3.2.0
  maven-war-version: 3.1.0 -> 3.2.2

- External maven plugins updated:
  pitest plugin: 1.2.4 -> 1.4.3
  jacoco plugin: 0.7.9 -> 0.8.2

- Libraries updated:
  H2: 1.4.196 -> 1.4.197
  Hibernate: 4.3.11.Final -> 5.3.7.Final
  Liquibase: 3.5.3 -> 3.6.2
  Postgresql JDBC driver: 42.1.1 -> 42.2.5

Note for Hibernate and Liquibase these are major updates and likely to introduce breaking changes into the code

## [1.7.1] - 2017-12-19
### Changed
- Remove copying of schema_catalog to rmal jar

## [1.7.0] - 2017-12-15
### Changed
- Adjusted the *build raml jar* plugin to include a schema_catalog.json if any exists

## [1.6.1] - 2017-11-20

### Changed
- Added `pitest` profile, which child projects can activate to enable mutation testing by setting `pitest.enabled` to true. 

## [1.6.0] - 2017-07-26

### Changed
- Build process improved
- Switched to Bintray for releases
- Simplified Dependent variable structure

## [1.5.0] - 2017-06-14

### Changed
- Plugins and Dependencies update to latest versions

## [1.4.1] - 2017-04-28

### Fixed
- Disable "add library to classpath" by *default* in maven-war-plugin

## [1.4.0] - 2017-02-14

### Added
- Added maven-plugin-plugin

## [1.3.0] - 2017-01-06

### Fixed
- Missing 'plugins.maven.assembly.version' property

## [1.2.0] - 2016-11-14

### Added
- Added raml-jar profile

## [1.1.0] - 2016-11-01

### Added
 - Common plugin configuration to POM

## [1.0.0] - 2016-07-28

### Added
- Initial release of parent POM for open source Maven projects

[Unreleased]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.6.1...HEAD
[1.6.1]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.6.0...release-1.6.1
[1.6.0]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.5.0...release-1.6.0
[1.5.0]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.4.0...release-1.5.0
[1.4.1]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.4.0...release-1.4.1
[1.4.0]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.3.0...release-1.4.0
[1.3.0]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.2.0...release-1.3.0
[1.2.0]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.1.0...release-1.2.0
[1.1.0]: https://github.com/CJSCommonPlatform/maven-parent-pom/compare/release-1.0.0...release-1.1.0
[1.0.0]: https://github.com/CJSCommonPlatform/maven-parent-pom/commits/release-1.0.0
