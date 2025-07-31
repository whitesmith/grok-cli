# Grok CLI

A CLI tool that starts the anthropic-proxy server configured for xAI API with Grok model and then runs claude-code. When claude-code exits, the proxy is automatically stopped.

## Installation

```bash
npm install -g grok-cli
```

Or run directly with npx:

```bash
npx grok-cli
```

## Usage

```bash
# First time - will prompt for Grok API key and store it in keychain
grok

# Using command line option to set/update API key
grok --api-key your-grok-api-key

# With custom port
grok --port 3001

# With custom models
grok --reasoning-model "grok-4" --completion-model "grok-3"

# With custom base URL (without /v1)
grok --base-url https://custom-api-endpoint.com

# Enable debug logging
grok --debug

# Reset stored API key
grok --reset-key
```

## Options

- `-k, --api-key <key>`: Grok API key (will be stored in macOS keychain)
- `-p, --port <port>`: Port for the proxy server (default: 3000)
- `--base-url <url>`: Base URL for the API endpoint (default: https://api.x.ai)
- `--reasoning-model <model>`: Reasoning model to use (default: grok-4)
- `--completion-model <model>`: Completion model to use (default: grok-3)
- `--debug`: Enable debug logging
- `--reset-key`: Reset the stored API key

## Features

- 🔐 **Secure Key Storage**: API keys are stored securely in macOS keychain
- 🤖 **Grok Model**: Uses xAI Grok 4 Instruct model by default
- 🚀 **Simple Setup**: Just run `grok` and it handles everything
- 🔄 **Auto Cleanup**: Automatically stops proxy when claude-code exits

## Requirements

- Node.js 14 or higher
- macOS (for keychain integration)
- `claude-code` installed and available in PATH

## Getting a Grok API Key

1. Visit [xAI Console](https://console.x.ai/)
2. Sign up or log in
3. Create a new API key
4. Run `grok` and enter your key when prompted

## How it works

1. Securely retrieves or prompts for your Grok API key
2. Starts a built-in proxy server that translates Anthropic API calls to Grok API format
3. Configures the proxy to use the specified API endpoint (default: `https://api.x.ai`) with Grok models
4. Sets the `ANTHROPIC_BASE_URL` environment variable to point to the local proxy
5. Launches claude-code with the configured environment
6. When claude-code exits, automatically stops the proxy server

## Troubleshooting

### Keychain Issues
If you encounter keychain permission issues, you can:
1. Run `grok --reset-key` to clear stored credentials
2. Use `grok --api-key your-key` to bypass keychain storage

### API Key Management
- To update your API key: `grok --api-key new-key`
- To reset stored key: `grok --reset-key`
- Keys are stored under service "grok-cli" in your keychain

## License

MIT

## Thanks

Anthropic proxy code is based on https://github.com/maxnowack/anthropic-proxy
