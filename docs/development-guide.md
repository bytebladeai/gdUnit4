# gdUnit4 Development Guide

**Generated:** 2026-01-13

## Prerequisites

| Requirement | Version | Notes |
|-------------|---------|-------|
| Godot Engine | 4.3 - 4.6 | Standard or .NET variant |
| .NET SDK | 9.0 | Required for C# components |
| C# Language | 13.0 | LangVersion in .csproj |
| Git | Any | Version control |
| gdlint | Latest | GDScript linting (optional) |

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/godot-gdunit-labs/gdUnit4.git
cd gdUnit4
```

### 2. Open in Godot Editor

1. Open Godot Engine (4.3+)
2. Import the `project.godot` file
3. The gdUnit4 plugin is auto-enabled

### 3. Build C# Components (for .NET)

If using Godot .NET variant:

```bash
dotnet build
```

## Running Tests

### From Godot Editor

- **Run All Tests:** Use the GdUnit Inspector panel
- **Run Single Test:** Right-click on test file in FileSystem
- **Run from Script Editor:** Right-click and select "Run Tests"

### From Command Line

**Linux/macOS:**
```bash
# Set Godot binary path
export GODOT_BIN=/path/to/godot

# Run all tests
./addons/gdUnit4/runtest.sh

# Run specific test path
./addons/gdUnit4/runtest.sh --add res://addons/gdUnit4/test/asserts
```

**Windows:**
```cmd
rem Set Godot binary path
set GODOT_BIN=C:\path\to\godot.exe

rem Run tests
addons\gdUnit4\runtest.cmd
```

**Direct Godot Command:**
```bash
godot --path . -s -d res://addons/gdUnit4/bin/GdUnitCmdTool.gd --add res://addons/gdUnit4/test/
```

## Project Structure for Development

```
gdUnit4/
├── addons/gdUnit4/
│   ├── src/              # Source code (edit here)
│   │   ├── asserts/      # Assertion implementations
│   │   ├── core/         # Core execution engine
│   │   └── ui/           # Editor UI components
│   └── test/             # Unit tests (write tests here)
├── documentation/        # Jekyll docs (edit for API changes)
└── gdUnit4.csproj        # C# project configuration
```

## Development Workflow

### 1. Select an Issue

- Find an open issue on GitHub
- Assign yourself and set status to "In Progress"
- Use issue number as branch name (e.g., `GD-111`)

### 2. Create Feature Branch

```bash
git checkout -b GD-XXX
```

### 3. Make Changes

- Follow [Godot GDScript Style Guide](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_styleguide.html)
- Follow [C# Coding Conventions](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)

### 4. Write Tests

- Add tests in `addons/gdUnit4/test/` mirroring the source structure
- Test file naming: `*Test.gd` or `*_test.gd`
- Use gdUnit4's own assertions

### 5. Run Tests Locally

```bash
./addons/gdUnit4/runtest.sh
```

### 6. Run Linting

```bash
gdlint addons/gdUnit4/src/
```

### 7. Submit Pull Request

- Link PR to issue
- Fill in "Why" and "What" sections
- Ensure CI passes

## CI/CD Pipelines

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| `ci-dev.yml` | Push to master | Run tests on Godot 4.5, 4.5.1 |
| `ci-pr.yml` | Pull request | Validate PR changes |
| `gdlint.yml` | Push/PR | GDScript style validation |
| `deploy-gh-pages.yml` | Push to master | Deploy documentation |

## Testing Matrix

The CI runs tests on:
- Godot 4.5 (standard)
- Godot 4.5 (.NET)
- Godot 4.5.1 (standard)
- Godot 4.5.1 (.NET)

## Configuration Files

| File | Purpose |
|------|---------|
| `.gdlintrc` | GDScript linter rules |
| `.editorconfig` | Editor formatting rules |
| `Directory.Build.props` | Shared MSBuild properties |
| `stylecop.json` | C# StyleCop configuration |
| `stylecop.ruleset` | C# analysis rules |
| `.runsettings` | .NET test settings (local) |
| `.runsettings-ci` | .NET test settings (CI) |

## Debugging

### Godot Debugger
1. Set breakpoints in Godot Script Editor
2. Run tests in debug mode (Inspector > Debug button)

### C# Debugging (VSCode/Rider)
1. Attach debugger to Godot process
2. See [documentation/doc/_csharp_project_setup/vstest-adapter.md](../documentation/doc/_csharp_project_setup/vstest-adapter.md)

## Documentation Updates

When changing APIs:

1. Update relevant markdown in `documentation/doc/`
2. Test locally with Jekyll:
   ```bash
   cd documentation
   bundle install
   bundle exec jekyll serve
   ```
3. Documentation auto-deploys on merge to master
