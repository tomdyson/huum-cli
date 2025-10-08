# Huum Sauna CLI

A command-line interface for managing Huum sauna devices remotely.

## Features

- 🔐 **Secure Authentication** - Store credentials safely in OS keyring
- 🔥 **Start Sessions** - Remotely start your sauna heating
- ⏹️  **Stop Sessions** - Turn off your sauna from the command line
- 📊 **Status Display** - View current and target temperatures with Rich formatting
- 🌡️  **Custom Temperatures** - Set target temperature (40-110°C)
- 🎯 **Auto-device Selection** - Automatically selects device if you have only one
- ⚡ **Fast & Reliable** - Automatic retries with exponential backoff

## Installation

Requires Python 3.11 or higher.

```bash
pip install huum-cli
```

Or with `uv`:

```bash
uv tool install huum-cli
```

### Development Installation

```bash
# Clone the repository
git clone https://github.com/tomdyson/huum-cli
cd huum-cli

# Install dependencies
uv sync

# Install the CLI in editable mode
uv pip install -e .
```

## Quick Start

### 1. Authenticate

```bash
huum auth login
```

You'll be prompted for your Huum account credentials. Your session will be stored securely in your system keyring.

### 2. Start Your Sauna

```bash
# Start with default temperature (85°C)
huum start

# Start with custom temperature
huum start --temperature 75
```

### 3. Stop Your Sauna

```bash
huum stop
```

## Commands

### Authentication

```bash
# Log in
huum auth login

# Log in with credentials
huum auth login --username user@example.com --password mypass

# Log out
huum auth logout
```

### Sauna Control

```bash
# Check status
huum status

# Start sauna
huum start [DEVICE_ID] [--temperature 85]

# Stop sauna
huum stop [DEVICE_ID]
```

### Device Management

If you have multiple devices, specify the device ID:

```bash
huum start my-sauna-id --temperature 80
huum stop my-sauna-id
```

## Configuration

Credentials are stored securely using your operating system's keyring:
- **macOS**: Keychain
- **Windows**: Windows Credential Manager
- **Linux**: GNOME Keyring/KWallet

## API

This CLI uses the Huum API (v1.2) at `https://sauna.huum.eu`.

See the [API documentation](https://app.swaggerhub.com/apis-docs/info716/HUUM/1.2) for more details.

## Development

Built with:
- **Typer** - CLI framework
- **httpx** - HTTP client
- **Pydantic** - Data validation
- **Rich** - Terminal formatting
- **keyring** - Secure credential storage

## Publishing a New Version

The project uses GitHub Actions to automatically publish to PyPI when you push a version tag.

### Prerequisites

1. Add your PyPI API token to GitHub repository secrets:
   - Go to https://github.com/tomdyson/huum-cli/settings/secrets/actions
   - Add a new secret named `PYPI_API_TOKEN`
   - Value: Your PyPI API token (starts with `pypi-`)

### Release Process

1. **Update version in `pyproject.toml`**:
   ```bash
   # Edit pyproject.toml and change version = "0.1.0" to new version
   ```

2. **Commit the version change**:
   ```bash
   git add pyproject.toml
   git commit -m "Bump version to 0.2.0"
   git push
   ```

3. **Create and push a git tag**:
   ```bash
   git tag v0.2.0
   git push origin v0.2.0
   ```

4. **GitHub Action runs automatically**:
   - Builds the package with `uv build`
   - Publishes to PyPI
   - Check progress at https://github.com/tomdyson/huum-cli/actions

### Version Numbering

Follow semantic versioning (MAJOR.MINOR.PATCH):
- **MAJOR**: Breaking changes (e.g., 1.0.0 → 2.0.0)
- **MINOR**: New features, backwards compatible (e.g., 0.1.0 → 0.2.0)
- **PATCH**: Bug fixes, backwards compatible (e.g., 0.1.0 → 0.1.1)

## License

MIT
