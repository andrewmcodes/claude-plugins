# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a personal marketplace repository for Claude Code plugins. It follows the Claude Code marketplace structure, with a central marketplace.json manifest that registers and configures plugins.

## Architecture

### Marketplace Structure

The repository uses a two-level structure:

1. **Marketplace Manifest**: `.claude-plugin/marketplace.json` contains:
   - Marketplace metadata (name, description, owner)
   - Plugin registry with entries for each plugin
   - Plugin-level configuration (LSP servers, categories, versions)

2. **Plugin Directories**: `plugins/{plugin-name}/` contains:
   - Individual plugin documentation (README.md)
   - Plugin-specific assets (if needed)

### Key Design Pattern

Plugin metadata lives in the marketplace.json, not in individual plugin.json files. Each plugin entry in the marketplace.json includes:
- Basic metadata (name, description, version, author)
- Source path pointing to the plugin directory
- Configuration (category, strict mode, LSP servers, etc.)

### LSP Server Configuration

LSP servers are configured directly in the marketplace.json under the `lspServers` field. Each LSP entry maps:
- A language identifier to a command
- File extensions to language types via `extensionToLanguage`

Example structure from ruby-lsp:
```json
"lspServers": {
  "ruby": {
    "command": "ruby-lsp",
    "extensionToLanguage": {
      ".rb": "ruby",
      "Gemfile": "ruby"
    }
  }
}
```

## Common Tasks

### Adding a New Plugin

1. Create a plugin directory: `plugins/{plugin-name}/`
2. Add a README.md with installation and usage instructions
3. Register the plugin in `.claude-plugin/marketplace.json`:
   ```json
   {
     "name": "plugin-name",
     "description": "Brief description",
     "version": "1.0.0",
     "author": { "name": "...", "email": "..." },
     "source": "./plugins/plugin-name",
     "category": "development"
   }
   ```

### Configuring an LSP Server Plugin

Add the `lspServers` field to the plugin entry in marketplace.json:
- Use language identifiers as keys
- Specify the command to launch the LSP
- Map file extensions to language types

### Updating Plugin Metadata

Edit `.claude-plugin/marketplace.json` - all plugin configuration lives here, not in separate plugin.json files.

## Repository Conventions

- Plugin names use kebab-case
- Each plugin has a README.md with installation instructions
- LSP plugins document supported file extensions
- Version numbers follow semver
- The marketplace owner email is support@andrewmcodes.com
