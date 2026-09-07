# Change Log
All notable changes to this project will be documented in this file, which follows the guidelines
on [Keep a CHANGELOG](http://keepachangelog.com/). This project adheres to
[Semantic Versioning](http://semver.org/).

## [Unreleased]

## [25.104.0] - 2026-09-07
First official (non-milestone) release of the Java 25 / WildFly 40 / Jakarta EE 11 line,
consolidating milestones `25.104.0-M1` to `25.104.0-M7` and the never-released Java 21 /
Jakarta EE 10 step that preceded them.

### Added
- `-Dnet.bytebuddy.experimental=true` to the surefire `argLine` for ByteBuddy Java 25 compatibility
- `WEB-INF/lib/resteasy-*.jar` to `maven-war-plugin` `<packagingExcludes>` — prevents bundled RESTEasy JARs from conflicting with WildFly's own RESTEasy module
- Jakarta EE version properties: `parsson.version`, `glassfish-json.version`, `jakarta.annotation-api.version`, `jakarta.inject-api.version`, `jakarta.jms-api.version`, `jakarta.xml.bind-api.version`, `persistence-api.version` and others

### Changed
- Targeted Java 25: `java.major.version` → `25` (so `maven-compiler-plugin` builds with `--release 25`) and `enforcer.java.version.range` → `[25,)`, aligning with `cpp-platform-maven-parent-pom`
- Targeted Jakarta EE 11: `java.ee.version` → `11`, `javaee-api.version` → `11.0.0`, `jee.api.version` → `11.0.0`
- Upgraded `maven-compiler-plugin` from `3.10.1` to `3.15.0` — required for full Java 25 source/target compatibility (Maven 3.9.16 default)
- Upgraded `maven-plugin-plugin` from `3.7.1` to `3.15.2` — required for Java 25 bytecode analysis (ASM 9.9)
- Upgraded `JaCoCo` from `0.8.8` to `0.8.14` — required for Java 25 class file (major version 69) instrumentation
- Upgraded `liquibase.version` from `4.10.0` to `5.0.3` — resolves Java 25 `VerifyError` in `liquibase-commercial:4.30.0` (`DbclHistoryCommandStep.setupSnakeYaml`); `liquibase-maven-plugin:5.0.3` has no dependency on `liquibase-commercial`
- Replaced `javax.xml.bind:jaxb-api` with `jakarta.xml.bind:jakarta.xml.bind-api` in the `coveralls-maven-plugin` dependency block
- Documented why `snakeyaml.version` stays pinned at `1.33`: snakeyaml 2.x drops the 7-arg `MappingNode` constructor that `org.raml:raml-parser` calls, causing `NoSuchMethodError` at test time. It must stay in lockstep with the `jackson-dataformat-yaml` `2.14.3` pin in `cp-maven-common-bom`
- Upgraded `maven-surefire-plugin` and `maven-failsafe-plugin` from `3.1.2` to `3.5.6` — Maven 3.9.16 defaults
- Upgraded `maven-jar-plugin` from `3.0.2` to `3.5.0` — Maven 3.9.16 default
- Upgraded `maven-install-plugin` from `2.5.2` to `3.1.4` — Maven 3.9.16 default
- Upgraded `maven-deploy-plugin` from `2.8.2` to `3.1.4` — Maven 3.9.16 default
- Upgraded `maven-war-plugin` from `3.1.0` to `3.5.1` — Maven 3.9.16 default
- Upgraded `maven-resources-plugin` from `3.0.2` to `3.4.0` — Maven 3.9.16 default
- Upgraded `maven-enforcer-plugin` from `3.0.0-M3` to `3.4.1`
- Upgraded `maven-assembly-plugin` from `3.0.0` to `3.7.1`
- Upgraded `maven-clean-plugin` from `3.0.0` to `3.2.0`
- Upgraded `maven-dependency-plugin` from `3.0.1` to `3.6.1`
- Upgraded `maven-site-plugin` from `3.6` to `3.12.1`
- Upgraded `maven-javadoc-plugin` from `2.10.4` to `3.6.3`
- Upgraded `maven-source-plugin` from `3.0.1` to `3.3.1`
- Upgraded `maven-wagon-plugin` from `2.10` to `3.5.3`
- Upgraded `versions-maven-plugin` from `2.5` to `2.16.2`
- Upgraded `maven-shade-plugin` from `3.0.0` to `3.6.0`
- Upgraded `build-helper-maven-plugin` from `3.0.0` to `3.6.0`
- Upgraded `buildnumber-maven-plugin` from `1.4` to `3.2.0`
- Upgraded `pitest` from `1.2.4` to `1.19.1`

### Removed
- `h2` and `liquibase-core` dependency management — moved to `cp-maven-common-bom`

### Fixed
- Removed the dead `<useLatestCommittedRevision>` entry from the `buildnumber-maven-plugin` config (unknown parameter — the real name is `useLastCommittedRevision`, and the value was the default `false`), eliminating the `[WARNING] Parameter 'useLatestCommittedRevision' is unknown for plugin 'buildnumber-maven-plugin'` build warning
- Removed the deprecated `maven-version` goal execution from the `build-helper-maven-plugin` configuration — Maven provides `${maven.version}` natively since 3.0.4 (MNG-4112), so the goal was redundant and logged `[WARNING] Goal 'maven-version' is deprecated ... So goal can be removed.` on every build

### Security
- Upgraded `postgresql.driver.version` from `42.3.2` to `42.7.7` — resolves CVE-2022-31197 (High) and CVE-2024-1597 (Critical); first version with full PostgreSQL 15/16 support

## [17.103.0] - 2025-07-11
### Changed
- Github migration to HMCTS Organisation
- Bumped h2.version to 2.3.232 

## [17.101.0] - 2025-01-08
### Changed
- Update postgresql.driver.version to 42.3.2

## [17.1.1] - 2024-06-12
### Added
- Add maven-sonar-plugin to pluginManagement

## [17.1.0] - 2023-07-05
### Changed
- Update maven-failsafe-plugin to 3.1.2
- Update maven-surefire-plugin to 3.1.2

## [17.0.0] - 2023-05-05
### Changed
- Update to OpenJdk 17
### Removed
- Remove illegal-access argument from plugin management (not valid for java 17) of sure fire plugin
- Remove illegal-access argument (not valid for java 17) from sure fire plugin

## [11.0.1] - 2023-02-01
### Changed
- Downgraded maven minimum version to 3.3.9 until the pipeline maven version is updated

## [11.0.0] - 2023-01-25
### Changed
- Bumped the version number to 11.0.0 to match the java 11 versions of the framework
- Update liquibase.version to 4.10.0
- Moved versions of liquibase dependencies to be properties of this pom:
  - snakeyaml.version: 1.30
  - picocli.version: 4.6.3
- Update to JEE 8
  - Update javaee-api version to 8.0.1
- Update postgresql.driver version to 42.2.18

## [8.0.0-M3] - 2020-12-11
### Added
- Added jaxb versions for java core dependencies now external in Java 11

## [8.0.0-M2] - 2020-12-11
### Fixed
- Added dependency on jaxb-api to coveralls-maven-plugin to fix ClassNotFoundException in Java 11

## [8.0.0-M1] - 2020-12-09
### Changed
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
