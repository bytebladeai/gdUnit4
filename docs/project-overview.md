# gdUnit4 Project Overview

**Generated:** 2026-01-13

## Project Identity

| Property | Value |
|----------|-------|
| **Name** | GdUnit4 |
| **Type** | Godot Unit Testing Framework |
| **Version** | 6.1.0 |
| **Author** | Mike Schulze |
| **License** | MIT |
| **Repository** | https://github.com/godot-gdunit-labs/gdUnit4 |

## Purpose

GdUnit4 is an embedded unit testing framework designed for testing GDScript, C# scripts, and scenes in the Godot 4.x engine. It supports Test-Driven Development (TDD) workflows and integrates directly into the Godot editor.

## Technology Stack Summary

| Layer | Technology |
|-------|------------|
| Platform | Godot Engine 4.3 - 4.6 |
| Primary Language | GDScript (221 source files) |
| Secondary Language | C# (.NET 9.0) |
| Documentation | Jekyll (GitHub Pages) |
| CI/CD | GitHub Actions (7 workflows) |

## Architecture Type

**Godot Editor Plugin (Addon)** with layered architecture:

```
┌────────────────┐
│   UI Layer     │  Editor Inspector, Console, Settings
├────────────────┤
│   Core Layer   │  Test Discovery, Execution, Reporting
├────────────────┤
│   API Layer    │  Assertions, Mocking, SceneRunner
├────────────────┤
│   CLI Layer    │  Command-line tool for CI/CD
└────────────────┘
```

## Repository Structure

- **Type:** Monolith
- **Parts:** 1 (single cohesive addon)
- **Location:** `addons/gdUnit4/`

## Key Features

### Core Testing
- GDScript and C# test support
- Embedded test inspector in Godot editor
- Automatic test discovery
- Fluent assertion syntax

### Advanced Capabilities
- Mocking and spying
- Parameterized tests
- Test fuzzing
- SceneRunner for scene testing
- Session hooks for custom reporting

### CI/CD Integration
- Command-line test runner
- JUnit XML report generation
- HTML report generation
- GitHub Action marketplace integration

## Quick Links

| Document | Description |
|----------|-------------|
| [Architecture](./architecture.md) | Technical architecture details |
| [Source Tree](./source-tree-analysis.md) | Directory structure analysis |
| [Development Guide](./development-guide.md) | Setup and contribution guide |

## External Documentation

| Resource | Location |
|----------|----------|
| API Documentation | https://godot-gdunit-labs.github.io/gdUnit4/latest/ |
| Installation Guide | https://godot-gdunit-labs.github.io/gdUnit4/latest/first_steps/install/ |
| C# Setup | https://godot-gdunit-labs.github.io/gdUnit4/latest/csharp_project_setup/csharp-setup/ |
| GitHub Action | https://github.com/marketplace/actions/gdunit4-test-runner-action |

## Supported Godot Versions

| GdUnit4 Version | Godot Version |
|-----------------|---------------|
| master (v6.1) | v4.6.beta2 |
| v6.x+ | v4.5, v4.5.1 |
| v5.x+ | v4.3, v4.4, v4.4.1 |
| v4.4.0+ | v4.2.0, v4.3, v4.4.dev2 |

## Community

- **Discord:** https://discord.gg/rdq36JwuaJ
- **GitHub Issues:** Bug reports and feature requests
- **GitHub Discussions:** General feedback and questions
