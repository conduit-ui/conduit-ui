# Conduit

**Your Personal Developer API Gateway**

Conduit is an extensible CLI with a component-based architecture that unifies your developer workflows. Built on Laravel Zero, it provides a microkernel that can be extended with isolated components for GitHub, music, Slack, and more.

## The Vision

> One CLI. All your developer tools. Beautifully orchestrated.

Instead of juggling `gh`, `spotify`, `slack`, and dozens of other CLIs, Conduit provides a unified interface with intelligent context awareness. Your music pauses when you start a focus session. Your Slack status updates when you start a PR review. Your task manager knows what branch you're on.

## Core Repositories

| Repository | Description |
|------------|-------------|
| [**conduit**](https://github.com/conduit-ui/conduit) | Main CLI application - the microkernel |
| [**core**](https://github.com/conduit-ui/core) | Shared services, interfaces, and component management |
| [**connector**](https://github.com/conduit-ui/connector) | GitHub API connector built with Saloon |

## Component Packages

| Component | Purpose |
|-----------|---------|
| [**issues**](https://github.com/conduit-ui/issues) | GitHub issues management |
| [**prs**](https://github.com/conduit-ui/prs) | Pull request workflows |
| [**commits**](https://github.com/conduit-ui/commits) | Commit history interface |
| [**repos**](https://github.com/conduit-ui/repos) | Repository management |
| [**actions**](https://github.com/conduit-ui/actions) | GitHub Actions interface |

## Architecture

```
conduit (microkernel)
├── core (shared interfaces & services)
├── connector (API layer)
└── components/ (isolated, versioned packages)
    ├── issues
    ├── prs
    ├── commits
    └── ...
```

**Key Principles:**
- **Isolated Components**: Each component manages its own dependencies
- **Typed Interfaces**: Domain-specific contracts (MusicProvider, VersionControl, Communication)
- **Git-Tag Versioning**: Proper semver with rollback capability
- **Clean Core**: Main composer.json never polluted by component deps

## Current Focus

We're building the foundation for a truly extensible developer experience:

1. **Component Installation System** - Git-tag based isolation with semver support
2. **Typed Interface Foundation** - Domain-specific contracts replacing generic interfaces
3. **GitHub Integration** - Issues, PRs, Actions, and workflow automation

## Quick Start

```bash
# Install Conduit
composer global require conduit-ui/conduit

# Install a component
conduit components install issues

# Use it
conduit issues list
conduit prs review
```

## Package APIs

All packages follow Taylor Otwell's expressive design philosophy:

```php
// Pull Requests
PullRequests::for('owner/repo')->open()->get();
$pr = PullRequests::find('owner/repo', 123);
$pr->approve('LGTM!')->merge('squash');

// Commits
Commits::query()
    ->repository('owner/repo')
    ->author('username')
    ->since('2025-01-01')
    ->get();

// Actions
Actions::for('owner/repo')->runs()->get();
Actions::for('owner/repo')->run(123)->rerun();

// Repositories
Repos::forOrg('laravel')->get();
$repo = Repos::find('laravel/framework');
$repo->branches();
```

## Contributing

Conduit is in active development. Check the [issues](https://github.com/conduit-ui/conduit/issues) for ways to contribute:

- **High Priority**: [SyncComponentsCommand fix](https://github.com/conduit-ui/conduit/issues/95)
- **Architecture**: [Component Installation Refactor](https://github.com/conduit-ui/conduit/issues/76)
- **Core**: [Define Interface Types](https://github.com/conduit-ui/conduit/issues/14)

---

*Built with Laravel Zero | PHP 8.3+*
