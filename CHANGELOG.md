# Makeflow Changelog

All notable changes to makeflow will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Changes that have been added but not yet released

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

[Unreleased]: https://github.com/ajdurancr/makeflow/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/ajdurancr/makeflow/releases/tag/v1.0.0
