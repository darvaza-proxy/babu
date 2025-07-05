# AI Agent Development Guidelines

This document provides guidelines for AI agents working on the Babu project.

## Project Context

Babu is an MIT-licensed SSH tunnel management system written in Go. It provides
a modern replacement for traditional SSH port forwarding with enhanced features
including virtual ports, integrated services, and centralised management.

## Language and Style

- **British English**: Use GB spelling (e.g., centralised, organisation)
- **Markdown**: Follow .markdownlint.json rules
- **Formatting**: Respect .editorconfig settings

## Key Technical Details

### Language and Framework

- **Language**: Go
- **Minimum Version**: Go 1.23
- **Key Libraries**: golang.org/x/crypto/ssh
- **Build System**: Makefile

### Architecture Overview

1. **Virtual Port System**: Ports are logical identifiers, not TCP bindings
2. **Multi-User Support**: Each device user has isolated configuration
3. **Git-Backed Config**: All configuration stored in git repositories
4. **Service Integration**: NTP, DNS, SOCKS5 over SSH channels

## Development Guidelines

### 1. Commit Messages

Use descriptive commit messages with proper sign-off. Never include AI
attribution or generation markers. e.g.

First, create the commit message file using:

Write `./.commit-msg-docs-architecture` with content:

```text
docs: enhance architecture documentation

- Add virtual port details
- Update component descriptions
- Fix formatting issues
```

Then commit specific files (git adds Signed-off-by with -s):

```bash
git commit -sF ./.commit-msg-docs-architecture docs/README.md docs/architecture/
rm ./.commit-msg-docs-architecture
```

**Important**: Always commit specific files directly rather than staging
everything to avoid including unintended changes.

### 2. Pull Requests

When creating PRs, provide clear descriptions without AI attribution:

Write `./.pr-body-port-registry` with content:

```markdown
## Summary

- Implement in-memory virtual port registry
- Add port allocation logic
- Create lookup mechanisms

## Test Plan

- Unit tests for port allocation
- Integration tests for concurrent access
- Performance benchmarks
```

And create the PR:

```bash
gh pr create --title "feat: implement virtual port registry" --body-file ./.pr-body-port-registry
rm ./.pr-body-port-registry
```

### 3. Editor Configuration

The project uses specific formatting rules:

- **Tabs**: Size 4 for Go source, size 8 for everything else
- **Spaces**: For YAML, JSON, Markdown (size 2)
- **Go files**: Tab size 4
- **Line length**: Maximum 80 characters
- **Line endings**: LF (Unix-style)
- **Final newline**: Always present
- **Trailing whitespace**: Always removed

### 4. Markdown Standards

Follow .markdownlint.json rules:

- **MD013**: Line length max 80 chars (except tables)
- **MD024**: Allow duplicate headings if not siblings
- **Blank lines**: Insert before and after headings, code blocks, and lists
- **Lists**: Use 1, 2, 3 for ordered lists
- **Links**: Prefer reference-style at document end

### 5. Code Conventions

When implementing features:

1. **Check Existing Patterns**: Always examine existing code first
2. **Follow Project Style**: Match indentation, naming, and structure
3. **Use Approved Dependencies Only**: Prefer the standard library and the
   darvaza project libraries.
   Avoid adding new external modules without prior discussion.
4. **Avoid Comments**: Only add comments when explicitly requested

### 6. File Operations

Efficient patterns for common tasks:

```bash
# Remove trailing whitespace from markdown files
git ls-files . | grep -E '\.md$' | xargs -r sed -i -e 's|[ \t]\+$||'

# Run markdownlint
pnpx markdownlint-cli "**/*.md" --fix

# Check git status efficiently
git status --porcelain
```

### 7. Working with Git

Important git practices:

1. **Signed Commits**: Use `-s` flag (git adds Signed-off-by automatically)
2. **Force Push**: Use `--force-with-lease` after fetching
3. **Branch Names**: Use descriptive names like `docs/topic` or `feat/feature`
4. **Specific Files**: Commit files directly, avoid bulk staging

Example workflow:

Create feature branch:

```bash
git checkout -b feat/virtual-ports
```

Make changes and commit specific files.

Write `./.commit-msg-port-registry` with content:

```text
feat: implement virtual port registry

- Add in-memory port mapping
- Create allocation logic
- Implement lookup methods
```

Commit with -s flag for automatic Signed-off-by:

```bash
git commit -sF ./.commit-msg-port-registry pkg/server/ports.go pkg/server/ports_test.go
rm ./.commit-msg-port-registry
```

and after the user agrees, push and create PR.

```bash
git push -u origin feat/virtual-ports
```

## Project-Specific Knowledge

### Port Allocation Scheme

- **25000-39999**: Registered devices (25000 + CRM ID)
- **40000-49999**: Pre-registered devices (40000 + counter)
- **50000-59999**: Quarantine range for compromised devices
- **Port 0**: Factory devices with default credentials

### Component Overview

1. **babu-server**: SSH server with virtual port support
   - Runs on port 2222
   - Dual mode: restricted for devices, full shell for admins
   - No TCP port binding for device forwards

2. **babu**: Client application
   - Replaces legacy SSH services
   - Integrated service support
   - Automatic reconnection

3. **babu-proxy**: Administrative access tool
   - ProxyCommand implementation
   - Device management CLI
   - Telemetry and monitoring

### Security Considerations

- Device users are restricted via authorized_keys options
- No shell access for device connections
- Bidirectional trust for maintenance operations
- Automatic compromise detection

## Common Tasks

### Adding Documentation

1. Create file in appropriate docs/ subdirectory
2. Add to docs/README.md index in logical order
3. Ensure markdownlint compliance
4. Commit with descriptive message

### Implementing Features

1. Research existing codebase patterns
2. Design following project conventions
3. Implement with tests
4. Update relevant documentation
5. Create PR with clear description

### Debugging Issues

1. Check git status and recent changes
2. Verify markdownlint compliance
3. Ensure proper file formatting
4. Test with actual SSH clients

## Important Reminders

- **No Attribution**: Never include AI attribution in commits, PRs, or code
- **Clean Room**: Implement from specification, not legacy code
- **Backwards Compatible**: Maintain compatibility during migration
- **Scale Aware**: Design for 10,000+ concurrent clients
- **Security First**: Never expose keys or sensitive data
- **British English**: Use GB spelling throughout

## Quick Reference

```bash
# Fix markdown issues
pnpx markdownlint-cli "**/*.md" --fix

# Remove trailing spaces
git ls-files . | xargs -r sed -i -e 's|[ \t]\+$||'
```

Create commit message file:

Write `./.commit-msg-feature` with content:

```text
type: description

- Detail one
- Detail two
```

Commit and clean up:

```bash
# Commit specific files with automatic Signed-off-by
git commit -sF ./.commit-msg-feature file1.go file2.go
rm ./.commit-msg-feature
```

Create PR:

```bash
gh pr create --title "title" --body-file ./.pr-body-feature
rm ./.pr-body-feature
```

## Repository

- GitHub: <https://github.com/darvaza-proxy/babu>
