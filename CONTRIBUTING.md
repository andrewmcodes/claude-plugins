# Contributing to claude-plugins

Thank you for your interest in contributing to this Claude Code plugin marketplace. This guide will help you add new plugins or improve existing ones.

## Table of Contents

- [Adding a New Plugin](#adding-a-new-plugin)
- [Plugin Structure Requirements](#plugin-structure-requirements)
- [Registering in Marketplace](#registering-in-marketplace)
- [LSP Server Configuration](#lsp-server-configuration)
- [Plugin Categories](#plugin-categories)
- [Testing Your Plugin](#testing-your-plugin)
- [Submitting Changes](#submitting-changes)

## Adding a New Plugin

### Step 1: Create Plugin Directory

Create a new directory under `plugins/` using kebab-case naming:

```bash
mkdir -p plugins/your-plugin-name
```

### Step 2: Create Plugin README

Every plugin **must** include a `README.md` with:

- Brief description
- Supported file extensions (for LSP plugins)
- Installation instructions
- Usage guidelines
- Links to official documentation

**Example structure:**

```markdown
# your-plugin-name

Brief description of what the plugin does.

## Supported Extensions

List file extensions this plugin handles (if applicable).

## Installation

### Via package manager

Installation instructions for the underlying tool.

## Usage

How the plugin enhances Claude Code workflows.

## More Information

- Links to official documentation
- GitHub repository
```

See [`plugins/ruby-lsp/README.md`](./plugins/ruby-lsp/README.md) as a reference.

### Step 3: Register Plugin in Marketplace

Add your plugin entry to `.claude-plugin/marketplace.json` in the `plugins` array:

```json
{
  "name": "your-plugin-name",
  "description": "Brief one-line description",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "your.email@example.com"
  },
  "source": "./plugins/your-plugin-name",
  "category": "development",
  "strict": false
}
```

**Required fields:**
- `name` - Plugin identifier (kebab-case)
- `description` - One-line summary
- `version` - Semantic version (e.g., "1.0.0")
- `author.name` - Your name
- `author.email` - Your email
- `source` - Path to plugin directory (always `./plugins/{name}`)
- `category` - One of the valid categories (see below)

**Optional fields:**
- `strict` - Whether to enforce strict validation (default: false)
- `lspServers` - LSP server configuration (see below)

## Plugin Structure Requirements

### Directory Layout

```
plugins/your-plugin-name/
├── README.md              # Required
├── commands/              # Optional: slash commands
├── agents/                # Optional: subagents
├── skills/                # Optional: skills
└── hooks/                 # Optional: lifecycle hooks
```

### File Naming Conventions

- **Plugin names:** Use kebab-case (e.g., `ruby-lsp`, `python-tooling`)
- **Files:** Use kebab-case for all files (e.g., `setup-env.md`, `run-tests.sh`)
- **README.md:** Always capitalized exactly as `README.md`

### Version Numbers

Follow [Semantic Versioning](https://semver.org/):

- **1.0.0** - Initial release
- **1.1.0** - New features (backward compatible)
- **1.0.1** - Bug fixes
- **2.0.0** - Breaking changes

## Registering in Marketplace

All plugin metadata lives in `.claude-plugin/marketplace.json`, **not** in separate `plugin.json` files.

### Basic Plugin Entry

```json
{
  "name": "example-plugin",
  "description": "Example plugin for demonstration",
  "version": "1.0.0",
  "author": {
    "name": "Andrew Mason",
    "email": "support@andrewmcodes.com"
  },
  "source": "./plugins/example-plugin",
  "category": "development"
}
```

### Marketplace File Structure

The marketplace.json contains:

1. **Marketplace metadata:**
   ```json
   {
     "name": "andrewmcodes-claude-plugins",
     "description": "Directory of personal Claude Code extensions",
     "owner": {
       "name": "Andrew Mason",
       "email": "support@andrewmcodes.com"
     }
   }
   ```

2. **Plugin registry:**
   ```json
   {
     "plugins": [
       { /* plugin entries */ }
     ]
   }
   ```

## LSP Server Configuration

For Language Server Protocol (LSP) plugins, add the `lspServers` field to your plugin entry:

### Structure

```json
{
  "name": "your-lsp-plugin",
  "description": "Language server for YourLanguage",
  "version": "1.0.0",
  "author": { /* ... */ },
  "source": "./plugins/your-lsp-plugin",
  "category": "development",
  "lspServers": {
    "your-language": {
      "command": "your-lsp-command",
      "extensionToLanguage": {
        ".ext": "your-language",
        ".other": "your-language",
        "ConfigFile": "your-language"
      }
    }
  }
}
```

### LSP Fields

- **Language identifier key** (`"your-language"`) - The language name
- **`command`** - The CLI command to launch the LSP server
- **`extensionToLanguage`** - Map of file extensions to language identifier
  - Keys can be file extensions (`.rb`) or specific filenames (`Gemfile`)
  - Values should match the language identifier key

### Example: Ruby LSP

```json
"lspServers": {
  "ruby": {
    "command": "ruby-lsp",
    "extensionToLanguage": {
      ".rb": "ruby",
      ".erb": "ruby",
      ".rake": "ruby",
      ".gemspec": "ruby",
      "Gemfile": "ruby",
      "Rakefile": "ruby",
      ".ru": "ruby"
    }
  }
}
```

### LSP Command Requirements

The command must:
- Be available in the user's PATH
- Support standard LSP protocol over stdin/stdout
- Be documented in the plugin README with installation instructions

## Plugin Categories

Choose the most appropriate category for your plugin:

- **`development`** - Language servers, build tools, linters, formatters
- **`productivity`** - Workflow automation, task management, project scaffolding
- **`data`** - Data processing, analysis tools, database clients
- **`ai`** - AI/ML integrations, model enhancements
- **`security`** - Security scanning, vulnerability analysis, secret detection
- **`testing`** - Test frameworks, test runners, coverage tools

## Testing Your Plugin

### Validation Checklist

Before submitting a PR, verify:

- [ ] Plugin directory exists at `plugins/{your-plugin-name}/`
- [ ] README.md exists and follows structure guidelines
- [ ] Plugin is registered in `.claude-plugin/marketplace.json`
- [ ] All required fields are present in plugin entry
- [ ] `source` path matches directory location
- [ ] Version follows semantic versioning
- [ ] Category is one of the valid options
- [ ] LSP configuration is correct (if applicable)
- [ ] JSON syntax is valid (use `jq` to check)

### Validate JSON Syntax

```bash
# Validate marketplace.json
jq empty .claude-plugin/marketplace.json

# Pretty-print to verify structure
jq . .claude-plugin/marketplace.json
```

### Test Installation

Test your plugin installation locally:

```bash
# Install from your local marketplace
/plugin install your-plugin-name@andrewmcodes-claude-plugins

# Verify it appears in the list
/plugin list

# Test functionality
# (Use the plugin with relevant file types)
```

### GitHub Actions Validation

The repository includes automated validation that checks:

1. Valid JSON syntax
2. Required marketplace fields
3. Required plugin fields
4. Plugin directories exist
5. Plugin READMEs exist

These checks run automatically on pull requests.

## Submitting Changes

### Commit Message Format

Use conventional commits for clear history:

- `feat: add python-lsp plugin` - New plugin
- `fix: correct ruby-lsp file extensions` - Bug fix
- `docs: update ruby-lsp README` - Documentation
- `chore: update marketplace metadata` - Maintenance

### Pull Request Process

1. **Fork and branch:**
   ```bash
   git checkout -b feat/add-your-plugin
   ```

2. **Make changes:**
   - Create plugin directory
   - Add README.md
   - Register in marketplace.json

3. **Validate:**
   - Run validation checks
   - Test installation

4. **Commit:**
   ```bash
   git add .
   git commit -m "feat: add your-plugin-name"
   ```

5. **Push and create PR:**
   ```bash
   git push origin feat/add-your-plugin
   # Create PR on GitHub
   ```

6. **PR labels:**
   - Add appropriate labels: `feat`, `plugin`, `docs`, etc.
   - Reference any related issues

### Review Process

Your PR will be reviewed for:

- Correct marketplace.json structure
- Plugin documentation quality
- Proper LSP configuration (if applicable)
- Adherence to naming conventions
- Passing automated validation

## Questions?

For questions or help:

- Open an issue on GitHub
- Email support@andrewmcodes.com
- Reference existing plugins as examples

Thank you for contributing!
