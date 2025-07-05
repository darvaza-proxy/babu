# Babu

[![Go Reference][godoc-badge]][godoc]
[![Go Report Card][go-report-badge]][go-report]
[![License: MIT][license-badge]][license]

> [!WARNING]
> This project is currently in the design phase and not ready for use.

## Overview

The **Babu** Project, from the [Akkadian][akkad-wikipedia] *bābu*
meaning *gate*, is a scalable SSH tunnel management system designed
to handle thousands of client connections with integrated services
and centralised management.

Babu provides three core components:

1. **`babu-server`** - SSH server replacing OpenSSH with dual functionality:
   - Virtual ports for device clients (no TCP binding)
   - Full shell access for administrators
2. **`babu`** - Specialised SSH client with integrated service support
3. **`babu-proxy`** - Tool for admin access to devices via virtual ports

## Key Features

- **Scalable Architecture**: Designed to handle 10,000+ concurrent clients
- **Port-Based Identity**: Unique port assignments for client identification
- **Integrated Services**: NTP, DNS, and SOCKS5 proxies over SSH
- **Git-Backed Configuration**: Version-controlled client management
- **Automatic Re-keying**: Detects and handles compromised keys

## Components

### `babu-server`

A complete SSH server implementation with innovative virtual port technology:

- **For devices**: Handles `-R` port forwarding without TCP binding
  - Virtual ports enable unlimited device connections
  - Device user `babu` has restricted access via `authorized_keys`
  - Compatible with standard SSH clients
- **For administrators**: Provides full shell access
  - Root and admin users get normal SSH shells
  - System management capabilities
- Provides integrated services (NTP, DNS, SOCKS5) via SSH channels
- Manages client registration and re-keying
- Detects key compromise through concurrent usage

### `babu-proxy`

A reverse proxy tool that:

- Enables administrators to connect to client SSH services
- Lists available clients and their connection status
- Creates port forwarding for client-side services
- Integrates with SSH `ProxyCommand` for transparent access

### `babu`

The intelligent SSH client that:

- Manages persistent connections to Babu servers
- Handles automatic pre-registration with factory keys
- Acts as local proxy for DNS, NTP, and SOCKS5 services
- Maintains connection reliability with automatic reconnection

## Pre-registration Process

New clients can self-register using factory keys:

1. Client connects with a shared factory key
2. Client generates a unique SSH key pair
3. Server assigns a unique name and port ID
4. Client uses assigned identity for future connections
5. Factory hostname can be updated to assigned name

## Quick Start

```bash
# Install Babu
go install darvaza.org/babu/cmd/babu@latest
go install darvaza.org/babu/cmd/babu-server@latest
go install darvaza.org/babu/cmd/babu-proxy@latest

# Start the server
babu-server --config /etc/babu/server.yaml

# Connect a client
babu connect --server babu.example.com --port 30001
```

## Documentation

Comprehensive documentation is available in the [docs/][docs] directory:

- [Getting Started][getting-started] - Installation and configuration
- [Architecture][architecture] - System design and scaling
- [Operations][operations] - Deployment and migration guides
- [Development][development] - Building and contributing
- [Reference][reference] - CLI and configuration reference

## Requirements

- Go 1.23 or later
- Linux, macOS, or BSD operating system
- Git (for configuration backend)

## Building from Source

```bash
# Clone the repository
git clone https://github.com/darvaza-proxy/babu.git
cd babu

# Build all components
make

# Run tests
make test

# Install to $GOPATH/bin
make install
```

## Contributing

We welcome contributions! Please see our [Contributing Guide][contributing]
for details on:

- Code of Conduct
- Development workflow
- Coding standards
- Testing requirements

## License

Babu is released under the [MIT License][license-file].

## Support

- **Documentation**: See the [docs/][docs] directory
- **Issues**: [GitHub Issues][babu-issues]
- **Discussions**: [GitHub Discussions][babu-discussions]
- **Security**: See [SECURITY.md][security]

## Acknowledgements

Babu is built on the excellent [golang.org/x/crypto/ssh][go-ssh]
library and benefits from the Go community's work on SSH tooling.

<!-- references -->
[akkad-wikipedia]: https://en.wikipedia.org/wiki/Akkad_(city)

[godoc-badge]: https://pkg.go.dev/badge/darvaza.org/babu.svg
[godoc]: https://pkg.go.dev/darvaza.org/babu
[go-report-badge]: https://goreportcard.com/badge/darvaza.org/babu
[go-report]: https://goreportcard.com/report/darvaza.org/babu
[license-badge]: https://img.shields.io/badge/License-MIT-yellow.svg
[license]: https://opensource.org/licenses/MIT

[docs]: docs/
[getting-started]: docs/getting-started/
[architecture]: docs/architecture/
[operations]: docs/operations/
[development]: docs/development/
[reference]: docs/reference/
[contributing]: CONTRIBUTING.md
[license-file]: LICENSE.txt
[security]: SECURITY.md

[babu-issues]: https://github.com/darvaza-proxy/babu/issues
[babu-discussions]: https://github.com/darvaza-proxy/babu/discussions

[go-ssh]: https://pkg.go.dev/golang.org/x/crypto/ssh
