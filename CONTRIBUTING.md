# Contributing to Babu

We welcome contributions to the Babu project! This document outlines the
process for contributing to this repository.

## Code of Conduct

By participating in this project, you agree to abide by our Code of Conduct.
Please read CODE_OF_CONDUCT.md before contributing.

## How to Contribute

### Reporting Issues

- Check if the issue already exists in our issue tracker
- Use the issue templates when creating new issues
- Provide clear descriptions and reproducible steps
- Include relevant system information and logs

### Submitting Changes

1. **Fork the Repository**
   - Fork the project on GitHub
   - Clone your fork locally

2. **Create a Branch**

   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/issue-description
   ```

3. **Make Your Changes**
   - Follow the coding standards (see below)
   - Write or update tests as needed
   - Update documentation if required

4. **Commit Your Changes**

   ```bash
   git add .
   git commit -m "feat: add new feature" # or "fix: resolve issue"
   ```

   Follow conventional commit format:
   - `feat:` New feature
   - `fix:` Bug fix
   - `docs:` Documentation changes
   - `test:` Test changes
   - `refactor:` Code refactoring
   - `chore:` Maintenance tasks

5. **Push to Your Fork**

   ```bash
   git push origin your-branch-name
   ```

6. **Create a Pull Request**
   - Open a PR from your fork to our main branch
   - Fill out the PR template completely
   - Link any related issues

## Development Setup

### Prerequisites

- Go 1.23 or higher
- Git
- Make (optional but recommended)

### Building

```bash
# Clone the repository
git clone https://github.com/darvaza-proxy/babu.git
cd babu

# Build all binaries
make build

# Run tests
make test

# Run linters
make lint
```

## Coding Standards

### Go Code

- Follow standard Go formatting (`gofmt`)
- Use `golangci-lint` for additional checks
- Write idiomatic Go code
- Add comments for exported functions
- Keep functions focused and small

### Documentation

- Use clear, concise language
- Include code examples where helpful
- Keep line length under 80 characters
- Follow markdownlint rules

### Testing

- Write unit tests for new functionality
- Maintain or improve code coverage
- Include integration tests where appropriate
- Test edge cases and error conditions

## Review Process

1. All submissions require review
2. Maintainers will provide feedback
3. Address review comments
4. Once approved, maintainers will merge

## License

By contributing, you agree that your contributions will be licensed under
the MIT License (see LICENSE.txt).
