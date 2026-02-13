# claude-plugins

Personal marketplace for Claude Code plugins and extensions.

## About

This repository provides a curated collection of Claude Code plugins for development workflows. It follows the Claude Code marketplace structure, with plugins organized in a central manifest for easy discovery and installation.

## Available Plugins

### ruby-lsp

Ruby language server for enhanced code intelligence and diagnostics.

**Features:**
- Code completion and IntelliSense
- Go to definition
- Find references
- Document symbols
- Diagnostics and linting

**Supported Extensions:** `.rb`, `.erb`, `.rake`, `.gemspec`, `Gemfile`, `Rakefile`, `.ru`

[View Documentation](./plugins/ruby-lsp/README.md)

## Installation

### Prerequisites

- [Claude Code](https://claude.ai/code) CLI installed
- Plugin dependencies installed (varies by plugin)

### Using the Marketplace

Install plugins from this marketplace using the Claude Code CLI:

```bash
# Install a specific plugin
/plugin install ruby-lsp@andrewmcodes-claude-plugins

# View installed plugins
/plugin list
```

### Adding This Marketplace

If this is your first time using this marketplace, Claude Code may need to discover it. The marketplace is identified by the owner email `support@andrewmcodes.com`.

## Contributing

Want to add a new plugin or improve an existing one? See [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed guidelines on:

- Adding new plugins
- Plugin structure requirements
- LSP server configuration
- Validation and testing

## Repository Structure

```
.
├── .claude-plugin/
│   └── marketplace.json      # Marketplace manifest and plugin registry
├── plugins/
│   └── ruby-lsp/            # Individual plugin directories
│       └── README.md
├── CONTRIBUTING.md          # Plugin development guide
└── README.md               # This file
```

## Plugin Categories

Plugins are organized into categories:

- **development** - Language servers, build tools, linters
- **productivity** - Workflow automation, task management
- **data** - Data processing and analysis tools
- **ai** - AI/ML integrations and enhancements
- **security** - Security scanning and analysis
- **testing** - Test frameworks and runners

## License

MIT License - see [LICENSE](./LICENSE) for details.
