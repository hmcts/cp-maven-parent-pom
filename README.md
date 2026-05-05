# cp-maven-parent-pom

`uk.gov.justice:maven-parent-pom`

The root Maven parent POM for all Criminal Practice Platform (CPP) framework projects. It establishes the baseline build configuration inherited by every framework and platform project.

## Position in the hierarchy

```
maven-super-pom  (external)
└── maven-parent-pom  ← this project
    ├── maven-common-bom
    └── maven-framework-parent-pom
        └── ...
```

`cpp-platform-maven-parent-pom` also inherits directly from `maven-super-pom`, making both tracks siblings at the root.

## What this POM provides

**Java / Jakarta EE target**
- Java 21 (`<release>21</release>`)
- Jakarta EE 10
- Enforcer requires Java ≥ 21 and Maven ≥ 3.3.9

**Plugin management** (versions pinned for all inheriting projects)
- `maven-compiler-plugin` 3.10.1 — Java 21, full warnings + lint enabled
- `maven-surefire-plugin` / `maven-failsafe-plugin` 3.1.2
- `jacoco-maven-plugin` 0.8.12 — coverage agent wired to all test and integration-test phases
- `maven-jar-plugin` 3.0.2 — SCM and CI metadata stamped into every JAR manifest
- `maven-war-plugin` 3.1.0 — resteasy JARs excluded from WAR (provided by WildFly)
- `maven-enforcer-plugin` 3.0.0-M3 — Java version, Maven version, and plugin-version rules active by default
- `maven-dependency-plugin`, `maven-resources-plugin`, `maven-assembly-plugin`, `maven-source-plugin`, `maven-javadoc-plugin`, `buildnumber-maven-plugin`, `build-helper-maven-plugin`, `versions-maven-plugin`, `pitest-maven`, `sonar-maven-plugin`

**Profiles**
| Profile | Activation | Effect |
|---|---|---|
| `raml-jar` | `src/raml` directory exists | Packages `src/raml/**` into a `raml` classifier JAR |
| `release` | `-Prelease` | Attaches sources and Javadocs |
| `pitest` | `-Dpitest.enabled=true` | Runs PIT mutation testing |
| `java-ee-7` | `java.ee.version=7` | Sets legacy EJB version (compatibility shim) |
| `windows` / `unix` | OS | Populates `ci.buildNode` from `%COMPUTERNAME%` or `$HOSTNAME` |

**Build conventions**
- `src/raml/json` is copied to `target/generated-test-resources/json`
- `src/raml/json/schema` is copied to `target/generated-resources/json/schema`

## Usage

All framework projects (`cp-framework-libraries`, `cp-microservice-framework`, `cp-event-store`, `cp-cake-shop`) inherit from `maven-framework-parent-pom` which in turn inherits from this POM. Service context projects (`cpp-context-*`) inherit via the `cpp-platform-*` hierarchy which also traces back here through `maven-super-pom`.

Do not declare this as a direct parent unless building a new top-level framework project.
