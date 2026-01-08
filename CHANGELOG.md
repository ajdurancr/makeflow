# Makeflow Changelog

All notable changes to makeflow will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Changes that have been added but not yet released

## [1.3.0] - 2026-01-07

### Added
- Slash commands for Claude Code and Cursor integration (17 commands total)
- Centralized command storage in `.agents/commands/` directory
- Symlinks from `.claude/commands/` and `.cursor/commands/` to central commands
- Comprehensive slash commands guide at `.makeflow/framework/SLASH-COMMANDS.md`
- Stage-prefixed command naming (00-04) for clear workflow progression
- End-to-end workflow examples in slash commands documentation
- Updated README.md with slash command usage examples throughout

### Changed
- Enhanced "Works with Any AI Tool" section in README with slash command examples
- Updated Project Structure section to show new `.agents/`, `.claude/`, and `.cursor/` directories
- Added slash commands to Quick Links and Documentation sections

### Commands Added
- **Stage 00 - Setup**: `/00-bootstrap-docs`, `/00-hook-docs`, `/00-update-makeflow`
- **Stage 01 - Intake**: `/01-from-bug`, `/01-from-idea`, `/01-from-ticket`
- **Stage 02 - Planning**: `/02-create-plan`, `/02-create-spec`, `/02-create-ticket`
- **Stage 03 - Execution**: `/03-execute-all-phases`, `/03-execute-phase`, `/03-execute-quick`, `/03-execute-task`, `/03-execute-task-without-tests`
- **Stage 04 - Delivery**: `/04-complete`, `/04-create-pr`, `/04-update-docs`

## [1.2.0] - 2026-01-07

### Added
- Documentation version tracking and synchronization workflows
- Validation workflow for documentation consistency

## [1.1.0] - 2025-12-14

### Added
- Missing execution workflow files (`execute-all-phases.md`, `execute-phase.md`)
- Enhanced framework documentation with references to new execution workflows
- Updated README with comprehensive workflow documentation

### Fixed
- Completed execution workflow documentation coverage

## [1.0.0] - 2025-12-14

### Added
- Initial release of makeflow
- 4-stage workflow system (Intake, Planning, Execution, Delivery)
- Work folder tracking with AGENTS.md entry point
- History summaries and INDEX for completed work
- Template system for prompts (bug, feature, refactor, agents)
- Framework documentation (DECISIONS.md, EXAMPLES.md, GUIDE.md, MULTI-TOOL.md)
- Documentation integration system with project/framework separation
- Comprehensive template system for project documentation
- Version tracking and update workflow

### Workflows
- **01-intake**: from-ticket, from-idea, from-bug
- **02-planning**: create-spec, create-plan, create-ticket
- **03-execution**: execute-task, execute-phase, execute-all-phases, execute-quick, execute-task-without-tests
- **04-delivery**: create-pr, update-docs, complete
- **00-setup**: hook-docs, bootstrap-docs, update-makeflow

### Documentation Structure
- `.makeflow/framework/` - Makeflow framework documentation
- `.makeflow/project/` - Host project documentation entry point
- `.makeflow/templates/project-docs/` - Documentation templates for host projects

[Unreleased]: https://github.com/ajdurancr/makeflow/compare/v1.3.0...HEAD
[1.3.0]: https://github.com/ajdurancr/makeflow/compare/v1.2.0...v1.3.0
[1.2.0]: https://github.com/ajdurancr/makeflow/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/ajdurancr/makeflow/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/ajdurancr/makeflow/releases/tag/v1.0.0
