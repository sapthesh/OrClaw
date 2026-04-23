# OrClaw - Personal AI Assistant
<a href="https://hits.sh/github.com/sapthesh/OrClaw/"><img alt="Hits" src="https://hits.sh/github.com/sapthesh/OrClaw.svg?view=today-total&style=for-the-badge&color=fe7d37"/></a> 

A privacy-focused personal AI assistant that integrates with your favorite chat apps and runs entirely on your own devices.

## Features

- **Multi-Platform Chat Integration**: WhatsApp, Slack, Telegram, Discord
- **Flexible AI Backends**: Local Ollama, Remote Ollama, OpenAI API
- **Hybrid Model Routing**: Automatically routes tasks based on complexity
- **Voice Processing**: Speech-to-text and text-to-speech support
- **Web Dashboard**: Simple UI for monitoring and configuration
- **Low Resource Usage**: Optimized for running 24/7 on modest hardware
- **CLI Setup Wizard**: Easy configuration without editing files

## Feature To-Do

- Fix config saving with encrypted storage
- Implement AgentSkills system
- Implement remote config/skills storage
- Implement chat interface with commands
- Create agents management system
- Add plugins and tools support
- Fix configuration page alignment

## Quick Start

### Prerequisites

- Node.js 20+ LTS
- (Optional) Ollama installed locally for private AI

### Installation

```bash
# Clone and install dependencies
cd personal-ai-assistant
npm install

# Run the setup wizard
npm run wizard

# Start the assistant
npm run dev
```

### Setup Wizard Walkthrough

The wizard will guide you through:

1. **Chat Platforms**: Select which apps to integrate (Telegram is easiest!)
2. **AI Providers**: Configure local Ollama, remote servers, or OpenAI API
3. **Voice Settings**: Enable speech processing
4. **Web Dashboard**: Set port and optional authentication

## Chat Platform Setup

### Telegram (Recommended for beginners)

1. Open Telegram and search for `@BotFather`
2. Send `/newbot` and follow prompts
3. Copy the bot token and enter it in the wizard

### Discord

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create a new application
3. Go to "Bot" tab and create a bot
4. Copy the token and enable required intents
5. Invite bot to your server with appropriate permissions

### Slack

1. Go to [Slack API](https://api.slack.com/apps)
2. Create a new app with "Bot User OAuth Token" scope
3. Install to workspace and copy the token

### WhatsApp

Requires a [Twilio](https://www.twilio.com/) account with WhatsApp Sandbox enabled.

## AI Provider Setup

### Local Ollama

1. Install Ollama from [ollama.ai](https://ollama.ai)
2. Pull a model: `ollama pull llama3.2`
3. The assistant will connect to `http://localhost:11434` automatically

### OpenAI API

1. Get an API key from [OpenAI](https://platform.openai.com/)
2. Enter it in the wizard or config file

## Configuration

The assistant uses a `config.json` file. You can edit it manually or through the web dashboard at `http://localhost:3000/config`.

Example config:

```json
{
  "chat": {
    "telegram": {
      "enabled": true,
      "botToken": "your-telegram-token"
    }
  },
  "ai": {
    "ollamaLocal": {
      "enabled": true,
      "model": "llama3.2:latest"
    }
  },
  "voice": {
    "sttEnabled": true,
    "ttsEnabled": true
  }
}
```

## Running as a Service

### Using PM2 (macOS/Linux)

```bash
# Build the project
npm run build

# Start with PM2
pm2 start pm2.config.js

# Auto-start on system boot
pm2 startup
pm2 save

# View logs
pm2 logs personal-ai-assistant
```

### Using systemd (Linux)

Create `/etc/systemd/system/personal-ai.service`:

```ini
[Unit]
Description=Personal AI Assistant
After=network.target

[Service]
Type=simple
User=your-user
WorkingDirectory=/path/to/personal-ai-assistant
ExecStart=/usr/bin/node dist/index.js
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
systemctl enable personal-ai
systemctl start personal-ai
```

## Web Dashboard

Visit `http://localhost:3000` to access:

- **Dashboard**: View status, message history, and provider health
- **Configuration**: Edit settings in a text editor
- **Logs**: View recent activity logs

## Project Structure

```
personal-ai-assistant/
├── src/
│   ├── config/       # Configuration management & wizard
│   ├── core/         # Message & model routing
│   ├── integrations/ # Chat platform handlers
│   ├── ai/           # AI provider clients
│   ├── voice/        # STT/TTS processing
│   ├── web/          # Dashboard server & views
│   └── storage/      # SQLite database
├── dist/             # Compiled output
├── logs/             # Application logs
├── data/             # Message database
└── config.json       # Configuration file
```

## Resource Usage

Typical usage on a modest VPS:

- **Memory**: ~150-300MB idle, ~500MB under load
- **CPU**: <1% idle, spikes during AI inference
- **Disk**: ~50MB for app + message history

## Troubleshooting

### "Ollama connection refused"

Ensure Ollama is running:
```bash
ollama serve
```

### "Bot token invalid"

Check that you copied the complete token without extra spaces or characters.

### Platform not responding

Check the web dashboard logs at `/logs` and verify:
1. Platform is enabled in config
2. Token is valid
3. Required permissions are granted

## License

MIT
