# Playflows

A powerful workflow engine for automating browser interactions with MCP Playwright tools. Originally designed for Grok.com automation, now generalized for any browser workflow automation.

## Features

- 🔐 Automated login with OAuth flow support
- 📸 Image upload and processing workflows
- ⏱️ Generation monitoring and progress tracking
- 💾 Automatic download of generated content
- 🖥️ CLI interface for easy automation
- 🔧 Configurable and extensible workflows
- 🎯 MCP Playwright tools integration

## Installation

```bash
npm install -g playflows
```

Or for local development:

```bash
npm install
```

## Usage

### CLI Commands

```bash
# Login to a service (manual OAuth)
playflows login

# Process an image (upload, generate, download)
playflows process <image-path>

# Or using npm scripts
npm run login
npm run process <image-path>
```

### Example

```bash
# Login first
playflows login

# Process an image
playflows process my-image.jpg
```

### Programmatic Usage

```javascript
const { Playflows } = require('playflows');

async function main() {
  const automation = new Playflows();

  try {
    await automation.initialize();
    await automation.login();
    await automation.uploadAndWaitForDownload('/path/to/image.jpg');
  } finally {
    await automation.close();
  }
}

main().catch(console.error);
```

## Configuration

The workflow engine supports configuration through:
- Environment variables
- Configuration files (`config.json`)
- Command-line arguments

### Example Configuration

```json
{
  "baseUrl": "https://grok.com",
  "timeout": 30000,
  "headless": false,
  "downloadPath": "./downloads"
}
```

## Architecture

- **WorkflowEngine**: Core engine that executes step-by-step workflows
- **GrokWorkflows**: Specific workflow implementations
- **ConfigManager**: Handles configuration and credential storage
- **Index.js**: Main interface and CLI tool

## Extending Playflows

Playflows is designed to be extensible. You can create custom workflows:

```javascript
const { WorkflowEngine } = require('playflows');

const engine = new WorkflowEngine();

// Define a custom workflow
engine.defineWorkflow('my-custom-flow', [
  { type: 'navigate', url: 'https://example.com' },
  { type: 'wait', time: 3 },
  { type: 'click', element: 'Submit Button' }
]);

// Execute the workflow
await engine.executeWorkflow('my-custom-flow');
```

## Security

- Credentials are stored locally and encrypted in memory
- Supports environment variables for production use
- Uses Playwright for secure browser automation

## Requirements

- Node.js >= 16.0.0
- Modern web browser (Chrome, Firefox, Safari, Edge)

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.