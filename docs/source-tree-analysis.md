# gdUnit4 Source Tree Analysis

**Generated:** 2026-01-13
**Project Type:** Godot Unit Testing Framework Library
**Repository Type:** Monolith

## Directory Structure Overview

```
gdUnit4/
├── addons/                          # Godot addon directory
│   └── gdUnit4/                     # Main addon package
│       ├── bin/                     # CLI tools (GdUnitCmdTool.gd)
│       ├── src/                     # Source code (221 GDScript files)
│       │   ├── asserts/             # Assertion implementations
│       │   ├── cmd/                 # Command-line argument parsing
│       │   ├── core/                # Core test execution engine
│       │   │   ├── command/         # Editor commands
│       │   │   ├── discovery/       # Test discovery system
│       │   │   ├── event/           # Event system (signals)
│       │   │   ├── execution/       # Test execution stages
│       │   │   ├── hooks/           # Session hooks & reporters
│       │   │   ├── parse/           # GDScript parsing utilities
│       │   │   ├── report/          # Report generation
│       │   │   ├── runners/         # Test session runners
│       │   │   ├── templates/       # Test suite templates
│       │   │   ├── thread/          # Threading utilities
│       │   │   └── writers/         # Output message writers
│       │   ├── doubler/             # Mock/spy implementations
│       │   ├── matchers/            # Argument matchers
│       │   ├── monitor/             # Memory/orphan monitoring
│       │   ├── network/             # Network utilities
│       │   ├── spy/                 # Spy implementations
│       │   ├── ui/                  # Godot editor UI components
│       │   │   ├── menu/            # Context menus
│       │   │   ├── parts/           # Inspector UI parts
│       │   │   ├── settings/        # Settings dialog
│       │   │   └── templates/       # UI templates
│       │   └── update/              # Update/migration system
│       └── test/                    # GDScript unit tests (self-testing)
│           ├── asserts/             # Assert tests
│           ├── core/                # Core system tests
│           ├── doubler/             # Mock/spy tests
│           ├── fuzzers/             # Fuzzer tests
│           ├── matchers/            # Matcher tests
│           ├── spy/                 # Spy tests
│           └── ui/                  # UI component tests
├── documentation/                   # Jekyll documentation site
│   ├── doc/                         # Markdown documentation
│   │   ├── _advanced_testing/       # Advanced topics (mocking, scene runner)
│   │   ├── _csharp_project_setup/   # C# integration guides
│   │   ├── _faq/                    # FAQ and solutions
│   │   ├── _first_steps/            # Getting started guides
│   │   ├── _testing/                # Core testing documentation
│   │   └── _tutorials/              # Tutorial guides
│   └── assets/                      # Documentation assets (images, CSS, JS)
├── .github/                         # GitHub configuration
│   ├── workflows/                   # CI/CD pipelines (7 workflows)
│   └── ISSUE_TEMPLATE/              # Issue templates
├── assets/                          # Project assets (images for contribution docs)
├── gdUnit4.csproj                   # C# project file (.NET 9.0)
├── gdUnit4.sln                      # Visual Studio solution
├── project.godot                    # Godot project configuration
└── plugin.cfg                       # Godot plugin descriptor (v6.1.0)
```

## Critical Directories

### `/addons/gdUnit4/src/` - Main Source Code
The heart of the framework containing all GDScript implementation:

| Directory | Purpose | Key Files |
|-----------|---------|-----------|
| `asserts/` | Assertion implementations | `GdUnitAssertImpl.gd`, `GdUnitStringAssertImpl.gd`, etc. |
| `core/` | Test execution engine | `GdUnitTestSuiteExecutor.gd`, `GdUnitSettings.gd` |
| `core/execution/` | Test lifecycle stages | `stages/GdUnitTestCaseExecutionStage.gd` |
| `core/discovery/` | Test discovery | `GdUnitTestDiscoverer.gd` |
| `core/runners/` | Session management | `GdUnitTestSessionRunner.gd` |
| `ui/` | Editor integration | `GdUnitInspector.gd`, `GdUnitConsole.gd` |
| `doubler/` | Mock/spy system | Mock generation and verification |

### `/addons/gdUnit4/bin/` - CLI Tools
Command-line interface for CI/CD integration:
- `GdUnitCmdTool.gd` - Main CLI entry point
- `runtest.sh` / `runtest.cmd` - Shell scripts for running tests

### `/documentation/` - Jekyll Documentation Site
Static site generator documentation:
- Published to GitHub Pages
- Contains API reference, tutorials, and guides

## Entry Points

| Entry Point | Type | Purpose |
|-------------|------|---------|
| `plugin.gd` | Editor | Godot editor plugin initialization |
| `bin/GdUnitCmdTool.gd` | CLI | Command-line test execution |
| `src/GdUnitTestSuite.gd` | API | Base class for test suites |
| `src/GdUnitSceneRunner.gd` | API | Scene testing interface |

## Key API Classes

### Public Assert Interfaces (in `src/`)
- `GdUnitAssert.gd` - Base assertion interface
- `GdUnitBoolAssert.gd` - Boolean assertions
- `GdUnitIntAssert.gd` - Integer assertions
- `GdUnitFloatAssert.gd` - Float assertions
- `GdUnitStringAssert.gd` - String assertions
- `GdUnitArrayAssert.gd` - Array assertions
- `GdUnitDictionaryAssert.gd` - Dictionary assertions
- `GdUnitObjectAssert.gd` - Object assertions
- `GdUnitSignalAssert.gd` - Signal assertions
- `GdUnitFileAssert.gd` - File system assertions
- `GdUnitFuncAssert.gd` - Function assertions
- `GdUnitVectorAssert.gd` - Vector assertions

### Core Classes (in `src/core/`)
- `GdUnitSettings.gd` - Configuration management
- `GdUnitTools.gd` - Utility functions
- `GdUnitSignals.gd` - Signal definitions
- `GdUnitResult.gd` - Result handling

## Test Structure

The framework tests itself using its own testing infrastructure:

```
/addons/gdUnit4/test/
├── asserts/          # Tests for assertion implementations
├── core/             # Tests for core execution engine
├── doubler/          # Tests for mock/spy functionality
├── fuzzers/          # Tests for fuzzing system
├── matchers/         # Tests for argument matchers
├── spy/              # Tests for spy functionality
└── ui/               # Tests for UI components
```

## CI/CD Workflows

Located in `.github/workflows/`:

| Workflow | Purpose |
|----------|---------|
| `ci-dev.yml` | Development branch CI |
| `ci-pr.yml` | Pull request validation |
| `ci-pr-example.yml` | Example project testing |
| `ci-pr-publish-report.yml` | Test report publishing |
| `gdlint.yml` | GDScript linting |
| `deploy-gh-pages.yml` | Documentation deployment |
| `workflow-cleanup.yml` | Workflow artifact cleanup |
