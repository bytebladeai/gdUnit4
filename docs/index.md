# gdUnit4 Project Documentation Index

**Generated:** 2026-01-13 | **Scan Level:** Quick | **Mode:** Initial Scan

## Project Overview

- **Type:** Monolith (Godot Editor Plugin/Addon)
- **Primary Language:** GDScript + C#
- **Architecture:** Layered Plugin Architecture
- **Version:** 6.1.0

## Quick Reference

- **Tech Stack:** GDScript, C# (.NET 9.0), Godot 4.3-4.6
- **Entry Point:** `addons/gdUnit4/plugin.gd` (editor), `bin/GdUnitCmdTool.gd` (CLI)
- **Architecture Pattern:** Layered with Plugin, Observer, and Stage patterns
- **Test Location:** `addons/gdUnit4/test/`

## Generated Documentation

| Document | Description |
|----------|-------------|
| [Project Overview](./project-overview.md) | High-level project summary and quick links |
| [Architecture](./architecture.md) | Technical architecture, component design, data flow |
| [Source Tree Analysis](./source-tree-analysis.md) | Directory structure with annotations |
| [Development Guide](./development-guide.md) | Setup, testing, and contribution instructions |

## Existing Documentation

This project has extensive existing documentation:

### In-Repository

| Document | Location | Description |
|----------|----------|-------------|
| README | [/README.md](../README.md) | Project overview, features, installation |
| Contributing | [/CONTRIBUTING.md](../CONTRIBUTING.md) | Contribution guidelines, coding style |
| PR Template | [/.github/pull_request_template.md](../.github/pull_request_template.md) | Pull request template |

### Jekyll Documentation Site (`/documentation/`)

| Section | Description |
|---------|-------------|
| [First Steps](../documentation/doc/_first_steps/) | Installation, settings, running tests |
| [Testing](../documentation/doc/_testing/) | Assertions, test suites, hooks |
| [Advanced Testing](../documentation/doc/_advanced_testing/) | Mocking, spying, fuzzing, SceneRunner |
| [C# Setup](../documentation/doc/_csharp_project_setup/) | C# configuration, VSTest adapter |
| [Tutorials](../documentation/doc/_tutorials/) | TDD tutorial, basics, examples |
| [FAQ](../documentation/doc/_faq/) | Solutions, CI integration |

### External Documentation

| Resource | URL |
|----------|-----|
| API Documentation | https://godot-gdunit-labs.github.io/gdUnit4/latest/ |
| GitHub Action | https://github.com/marketplace/actions/gdunit4-test-runner-action |
| Discord Server | https://discord.gg/rdq36JwuaJ |

## Getting Started

### For Users

1. **Install:** Follow the [installation guide](https://godot-gdunit-labs.github.io/gdUnit4/latest/first_steps/install/)
2. **Write Tests:** Extend `GdUnitTestSuite` and add `test_*` methods
3. **Run Tests:** Use the GdUnit Inspector in Godot or the CLI

### For Contributors

1. **Clone:** `git clone https://github.com/godot-gdunit-labs/gdUnit4.git`
2. **Setup:** Open `project.godot` in Godot 4.3+
3. **Test:** Run `./addons/gdUnit4/runtest.sh`
4. **Contribute:** See [Development Guide](./development-guide.md)

## Key Source Locations

| Purpose | Location |
|---------|----------|
| Public API | `addons/gdUnit4/src/*.gd` |
| Assertions | `addons/gdUnit4/src/asserts/` |
| Core Engine | `addons/gdUnit4/src/core/` |
| Editor UI | `addons/gdUnit4/src/ui/` |
| CLI Tool | `addons/gdUnit4/bin/` |
| Tests | `addons/gdUnit4/test/` |
| Documentation | `documentation/doc/` |

## CI/CD Workflows

| Workflow | Purpose |
|----------|---------|
| ci-dev.yml | Master branch testing |
| ci-pr.yml | Pull request validation |
| gdlint.yml | GDScript linting |
| deploy-gh-pages.yml | Documentation deployment |

---

*This documentation was generated for AI-assisted development. When creating brownfield PRDs or planning features, reference this index and the linked documents for project context.*
