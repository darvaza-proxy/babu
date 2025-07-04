# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog][keepachangelog],
and this project adheres to [Semantic Versioning][semver].

## [Unreleased]

### Added

- Initial project scaffolding with three core binaries:
  - `badu` - SSH client with Babu-specific features
  - `badu-server` - SSH server with port-based client identification
  - `badu-proxy` - Reverse SSH proxy for admin access to clients
- Build infrastructure (Makefile, version scripts, go.mod)
- Development configuration (.editorconfig, revive linting)
- CI/CD workflows (GitHub Actions build and Renovate)
- Documentation structure with placeholder files
- Contributing guidelines and Code of Conduct
- MIT License

<!-- references -->
[keepachangelog]: https://keepachangelog.com/en/1.1.0/
[semver]: https://semver.org/spec/v2.0.0.html
[Unreleased]: https://github.com/darvaza-proxy/babu/commits/main
