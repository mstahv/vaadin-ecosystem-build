# Vaadin Add-on Compatibility Tester

A JBang script for testing Vaadin add-ons against different Vaadin framework versions.

## Prerequisites

- Java 21 or higher
- [JBang](https://www.jbang.dev/) installed
- Git
- Maven

## Usage

Run the script directly with JBang:

```bash
./AddonTester.java
```

Or explicitly with JBang:

```bash
jbang AddonTester.java
```

### Options

| Option | Description | Default |
|--------|-------------|---------|
| `-v`, `--vaadin.version` | Vaadin version to test against | `25.0.5` |
| `-w`, `--work-dir` | Working directory for cloning projects | `work` |
| `-c`, `--clean` | Clean work directory before running | `false` |
| `-h`, `--help` | Show help message | |
| `-V`, `--version` | Print version info | |

### Examples

Test against the default Vaadin version:
```bash
./AddonTester.java
```

Test against a specific Vaadin version:
```bash
./AddonTester.java -v 24.6.0
```

Clean the work directory and run fresh:
```bash
./AddonTester.java --clean -v 25.0.5
```

## Adding Add-ons

Edit the `ADDONS` list in `AddonTester.java` to configure which add-ons to test:

```java
private static final List<AddonConfig> ADDONS = List.of(
    new AddonConfig("addon-name", "https://github.com/org/repo"),
    new AddonConfig("another-addon", "https://github.com/org/another-repo",
                    "branch-name", List.of("-DskipTests"), false, null)
);
```

### AddonConfig Fields

- `name` - Directory name for the cloned repository
- `repoUrl` - Git repository URL
- `branch` - Branch to checkout (optional, defaults to main)
- `extraMvnArgs` - Additional Maven arguments (optional)
- `ignored` - Skip this add-on if true
- `ignoreReason` - Reason for ignoring (shown in output)

## How It Works

1. Clones (or updates) each configured add-on repository into the work directory
2. Runs `mvn verify -Dvaadin.version=<version>` for each add-on
3. Reports success/failure status with timing information
4. Returns exit code 0 if all tests pass, 1 otherwise
