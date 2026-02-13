# ruby-lsp

Ruby language server for Claude Code, providing code intelligence and diagnostics.

## Supported Extensions

`.rb`, `.erb`, `.rake`, `.gemspec`, `Gemfile`, `Rakefile`, `.ru`

## Installation

### Via gem (Recommended)

```bash
gem install ruby-lsp
```

### Via mise

```bash
mise use -g gem:ruby-lsp
```

Verify installation:
```bash
mise exec -- ruby-lsp --version
```

### Via Bundler (Project-specific)

Add to your Gemfile:
```ruby
gem 'ruby-lsp', require: false
```

Then install:
```bash
bundle install
```

## Usage

Once installed, the ruby-lsp language server will automatically activate for Ruby files when using Claude Code. It provides:

- Code completion and IntelliSense
- Go to definition
- Find references
- Document symbols
- Diagnostics and linting

## More Information

- [ruby-lsp GitHub](https://github.com/Shopify/ruby-lsp)
- [ruby-lsp Documentation](https://shopify.github.io/ruby-lsp/)
