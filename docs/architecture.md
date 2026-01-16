# gdUnit4 Architecture Document

**Generated:** 2026-01-13
**Version:** 6.1.0
**Project Type:** Godot Unit Testing Framework

## Executive Summary

GdUnit4 is an embedded unit testing framework for Godot Engine 4.x, supporting both GDScript and C# test development. The framework provides a fluent assertion API, mocking/spying capabilities, scene testing via SceneRunner, and integrates directly into the Godot editor as a plugin.

## Technology Stack

| Category | Technology | Version | Purpose |
|----------|------------|---------|---------|
| Platform | Godot Engine | 4.3 - 4.6 | Runtime environment |
| Primary Language | GDScript | Godot 4.x | Core addon implementation |
| Secondary Language | C# | .NET 9.0, C# 13.0 | .NET integration |
| Plugin Framework | Godot Addon | plugin.cfg v6.1.0 | Editor integration |
| CI/CD | GitHub Actions | - | Automated testing |
| Documentation | Jekyll | GitHub Pages | API documentation |

## Architecture Pattern

**Layered Architecture with Plugin Pattern**

```
┌─────────────────────────────────────────────────────────────────┐
│                        Godot Editor                              │
│  ┌─────────────────────────────────────────────────────────────┐ │
│  │                    GdUnit4 Plugin                           │ │
│  │  ┌───────────────────┐  ┌────────────────────────────────┐ │ │
│  │  │    UI Layer       │  │      CLI Layer                 │ │ │
│  │  │  - GdUnitInspector│  │  - GdUnitCmdTool               │ │ │
│  │  │  - Settings Dialog│  │  - runtest.sh/cmd              │ │ │
│  │  └─────────┬─────────┘  └──────────────┬─────────────────┘ │ │
│  │            │                            │                   │ │
│  │            ▼                            ▼                   │ │
│  │  ┌───────────────────────────────────────────────────────┐ │ │
│  │  │                    Core Layer                          │ │ │
│  │  │  - Test Discovery    - Test Execution                  │ │ │
│  │  │  - Session Management - Report Generation              │ │ │
│  │  │  - Signal/Event System - Configuration                 │ │ │
│  │  └─────────────────────────────────────────────────────────┘ │ │
│  │            │                                                 │ │
│  │            ▼                                                 │ │
│  │  ┌───────────────────────────────────────────────────────┐ │ │
│  │  │                   API Layer                            │ │ │
│  │  │  - Assertions      - Mocking/Spying                    │ │ │
│  │  │  - SceneRunner     - Fuzzers                           │ │ │
│  │  │  - Argument Matchers - Test Hooks                      │ │ │
│  │  └───────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    User Test Suites                              │
│  class_name MyTest extends GdUnitTestSuite                       │
└─────────────────────────────────────────────────────────────────┘
```

## Component Overview

### 1. Plugin Entry Point (`plugin.gd`)

The Godot editor plugin entry point that:
- Registers the addon with the editor
- Initializes the UI components
- Sets up command handlers and shortcuts

### 2. UI Layer (`src/ui/`)

**Key Components:**
- `GdUnitInspector.gd` - Main test explorer panel
- `GdUnitConsole.gd` - Test output console
- `InspectorToolBar.gd` - Run/debug controls
- `GdUnitSettingsDialog.gd` - Configuration interface

**Pattern:** Observer pattern via Godot signals for UI updates

### 3. Core Layer (`src/core/`)

**Test Discovery (`core/discovery/`):**
- `GdUnitTestDiscoverer.gd` - Scans for test classes
- `GdUnitTestCase.gd` - Test case metadata
- `GdUnitGUID.gd` - Unique test identification

**Test Execution (`core/execution/`):**
- `GdUnitTestSuiteExecutor.gd` - Orchestrates test runs
- `GdUnitExecutionContext.gd` - Execution state management
- `stages/` - Lifecycle stage implementations:
  - `GdUnitTestSuiteBeforeStage.gd` - Suite setup
  - `GdUnitTestCaseBeforeStage.gd` - Test setup
  - `GdUnitTestCaseExecutionStage.gd` - Test execution
  - `GdUnitTestCaseAfterStage.gd` - Test teardown
  - `GdUnitTestSuiteAfterStage.gd` - Suite teardown

**Session Management (`core/runners/`):**
- `GdUnitTestSession.gd` - Test session state
- `GdUnitTestSessionRunner.gd` - Editor session runner
- `GdUnitTestCIRunner.gd` - CI/headless runner

**Event System (`core/event/`):**
- `GdUnitEvent.gd` - Base event class
- `GdUnitEventTestDiscoverStart/End.gd` - Discovery events
- `GdUnitSessionStart/Close.gd` - Session lifecycle

**Hooks (`core/hooks/`):**
- `GdUnitTestSessionHook.gd` - Session hook interface
- `GdUnitHtmlReporterTestSessionHook.gd` - HTML reports
- `GdUnitXMLReporterTestSessionHook.gd` - JUnit XML reports

### 4. API Layer (`src/`)

**Assertion Interfaces:**
```
GdUnitAssert (base)
├── GdUnitBoolAssert
├── GdUnitIntAssert
├── GdUnitFloatAssert
├── GdUnitStringAssert
├── GdUnitArrayAssert
├── GdUnitDictionaryAssert
├── GdUnitObjectAssert
├── GdUnitSignalAssert
├── GdUnitFileAssert
├── GdUnitFuncAssert
├── GdUnitVectorAssert
└── GdUnitResultAssert
```

**Assertion Pattern:** Fluent interface with chained method calls
```gdscript
assert_str("hello world").starts_with("hello").has_length(11)
```

**Test Base Class:**
- `GdUnitTestSuite.gd` - Base class users extend

**Scene Testing:**
- `GdUnitSceneRunner.gd` - Scene testing interface
- Supports input simulation (mouse, keyboard, touch)

**Mocking/Spying (`src/doubler/`, `src/spy/`):**
- Dynamic mock/spy generation at runtime
- Argument matchers for verification

### 5. CLI Layer (`bin/`)

- `GdUnitCmdTool.gd` - Command-line interface
- `runtest.sh` / `runtest.cmd` - Shell wrappers

## Data Flow

### Test Execution Flow

```
1. User triggers test run (UI/CLI)
         │
         ▼
2. GdUnitTestDiscoverer scans for tests
         │
         ▼
3. GdUnitTestSession created with test list
         │
         ▼
4. GdUnitTestSessionRunner orchestrates execution
         │
         ▼
5. For each test suite:
   a. GdUnitTestSuiteBeforeStage (before_all)
   b. For each test case:
      i.   GdUnitTestCaseBeforeStage (before)
      ii.  GdUnitTestCaseExecutionStage (test_*)
      iii. GdUnitTestCaseAfterStage (after)
   c. GdUnitTestSuiteAfterStage (after_all)
         │
         ▼
6. Results collected via GdUnitTestReportCollector
         │
         ▼
7. Session hooks generate reports (HTML/XML)
         │
         ▼
8. UI updated via signals
```

### Signal/Event Communication

```
GdUnitSignals (singleton)
    ├── gdunit_event (GdUnitEvent)
    ├── gdunit_set_test_failed
    ├── gdunit_message
    └── gdunit_client_connected/disconnected
```

## Configuration Management

**GdUnitSettings.gd** manages:
- UI preferences (inspector, console)
- Report generation settings
- Hook configurations
- Shortcut bindings
- Template customization

Settings stored in Godot's `project.godot` under `[gdunit4]` section.

## Extensibility Points

1. **Custom Assertions:** Extend `GdUnitAssert` base class
2. **Session Hooks:** Implement `GdUnitTestSessionHook` interface
3. **Custom Fuzzers:** Extend fuzzer base classes
4. **Test Templates:** Customize via Settings dialog

## Threading Model

- Tests run on main thread (Godot limitation)
- `GdUnitThreadManager.gd` provides context management
- Async operations use Godot's await/signal pattern

## External Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| gdUnit4.api | 5.1.0-rc3 | C# testing API |
| gdUnit4.test.adapter | 3.0.0 | VSTest integration |
| gdUnit4.analyzers | 1.0.0 | C# static analysis |
| Microsoft.NET.Test.Sdk | 18.0.1 | .NET test infrastructure |

## Key Design Decisions

1. **Fluent API:** Chainable assertions for readable tests
2. **Plugin Architecture:** Non-invasive integration with Godot
3. **Self-Testing:** Framework tests itself using its own APIs
4. **Dual Language Support:** GDScript primary, C# via separate package
5. **Signal-Based Communication:** Loose coupling via Godot signals
6. **Stage Pattern:** Execution lifecycle as discrete stages
