# HyperFocache 🧠⚡

Your External Brain, Amplified - An ADHD-optimized memory augmentation system for developers who leverage hyperfocus as a superpower.

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Installation](#installation)
  - [Requirements](#requirements)
  - [Cursor](#cursor)
  - [Windsurf](#windsurf)
  - [Claude Desktop](#claude-desktop)
  - [Claude Code](#claude-code)
  - [VS Code](#vs-code)
  - [Visual Studio 2022](#visual-studio-2022)
  - [Zed](#zed)
  - [Cline](#cline)
  - [Trae](#trae)
  - [Gemini CLI](#gemini-cli)
  - [BoltAI](#boltai)
  - [Augment Code](#augment-code)
  - [Roo Code](#roo-code)
  - [Zencoder](#zencoder)
  - [Amazon Q Developer CLI](#amazon-q-developer-cli)
  - [Qodo Gen](#qodo-gen)
  - [JetBrains AI Assistant](#jetbrains-ai-assistant)
  - [Warp](#warp)
  - [Opencode](#opencode)
  - [Copilot Coding Agent](#copilot-coding-agent)
  - [Kiro](#kiro)
  - [LM Studio](#lm-studio)
  - [Perplexity Desktop](#perplexity-desktop)
  - [Smithery](#smithery)
  - [Docker](#docker)
  - [Windows](#windows)
- [Feedback & Support](#feedback--support)
- [Getting Started](#getting-started)
- [About](#about)

## Overview

HyperFocache is a high-performance cognitive tool designed specifically for developers with ADHD. It provides seamless memory management and retrieval, helping you maintain context across interruptions, track your problem-solving journeys, and build a searchable knowledge base that grows with you.

## Key Features

- **20+ Memory Tools**: Comprehensive suite for saving, searching, evolving, and organizing memories
- **Semantic Search**: Find memories by meaning, not just keywords
- **Context Preservation**: Save and restore work states when switching tasks or getting interrupted
- **Problem-Solving Breadcrumbs**: Track your debugging journeys, including dead ends and breakthroughs
- **Memory Evolution**: Update existing memories without losing history
- **Intelligent Consolidation**: Automatically merge related memories to reduce clutter
- **Time-Based Retrieval**: Navigate your memory timeline effortlessly
- **Relationship Mapping**: Visualize connections between memories
- **ADHD-Optimized**: Built by and for developers with ADHD

## Installation

### Requirements

- Node.js >= v18.0.0 (for local installations)
- Cursor, Windsurf, Claude Desktop, or another MCP Client

> **Note**: HyperFocache is entirely remote-based, so most installations will use the remote server endpoints. For Docker-based installations, you'll need the mcp-remote fork with Docker support.

### Cursor

<details>
<summary><b>Install in Cursor</b></summary>

Go to: `Settings` -> `Cursor Settings` -> `MCP` -> `Add new global MCP server`

Since Cursor 1.0, you can use one-click installation or paste the configuration into your `~/.cursor/mcp.json` file.

#### Remote Server Connection (Recommended)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "url": "https://hyperfocache.offendingcommit.com/mcp"
    }
  }
}
```

#### Docker-based Connection (Alternative)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

</details>

### Windsurf

<details>
<summary><b>Install in Windsurf</b></summary>

Add this to your Windsurf MCP config file. See [Windsurf MCP docs](https://docs.windsurf.com/windsurf/mcp) for more info.

#### Remote Server Connection (Recommended)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "serverUrl": "https://hyperfocache.offendingcommit.com/sse"
    }
  }
}
```

#### Docker-based Connection (Alternative)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

</details>

### Claude Desktop

<details>
<summary><b>Install in Claude Desktop</b></summary>

Add this to your Claude Desktop `claude_desktop_config.json` file. See [Claude Desktop MCP docs](https://modelcontextprotocol.io/quickstart/user) for more info.

Since Claude Desktop primarily supports stdio connections, you'll need to use the Docker-based mcp-remote fork:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

</details>

### Claude Code

<details>
<summary><b>Install in Claude Code</b></summary>

Run this command. See [Claude Code MCP docs](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/tutorials#set-up-model-context-protocol-mcp) for more info.

#### Remote Server Connection (Recommended)

```sh
claude mcp add --transport http hyperfocache https://hyperfocache.offendingcommit.com/mcp
```

Or using SSE transport:

```sh
claude mcp add --transport sse hyperfocache https://hyperfocache.offendingcommit.com/sse
```

#### Docker-based Connection (Alternative)

```sh
claude mcp add hyperfocache -- docker run -i --rm -v mcp-auth:/home/mcp/.mcp-auth ghcr.io/offendingcommit/mcp-remote:latest https://hyperfocache.offendingcommit.com/sse
```

</details>

### VS Code

<details>
<summary><b>Install in VS Code</b></summary>

Add this to your VS Code MCP config file. See [VS Code MCP docs](https://code.visualstudio.com/docs/copilot/chat/mcp-servers) for more info.

#### Remote Server Connection (Recommended)

```json
"mcp": {
  "servers": {
    "hyperfocache": {
      "type": "http",
      "url": "https://hyperfocache.offendingcommit.com/mcp"
    }
  }
}
```

#### Docker-based Connection (Alternative)

```json
"mcp": {
  "servers": {
    "hyperfocache": {
      "type": "stdio",
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

</details>

### Visual Studio 2022

<details>
<summary><b>Install in Visual Studio 2022</b></summary>

Follow the [Visual Studio MCP Servers documentation](https://learn.microsoft.com/visualstudio/ide/mcp-servers?view=vs-2022).

Add this to your Visual Studio MCP config file:

```json
{
  "mcp": {
    "servers": {
      "hyperfocache": {
        "type": "http",
        "url": "https://hyperfocache.offendingcommit.com/mcp"
      }
    }
  }
}
```

</details>

### Zed

<details>
<summary><b>Install in Zed</b></summary>

Add this to your Zed `settings.json`. See [Zed Context Server docs](https://zed.dev/docs/assistant/context-servers) for more info.

```json
{
  "context_servers": {
    "hyperfocache": {
      "command": {
        "path": "docker",
        "args": [
          "run",
          "-i",
          "--rm",
          "-v",
          "mcp-auth:/home/mcp/.mcp-auth",
          "ghcr.io/offendingcommit/mcp-remote:latest",
          "https://hyperfocache.offendingcommit.com/sse"
        ]
      },
      "settings": {}
    }
  }
}
```

</details>

### Cline

<details>
<summary><b>Install in Cline</b></summary>

Add this to your Cline MCP settings:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

</details>

### Trae

<details>
<summary><b>Install in Trae</b></summary>

Use the Add manually feature and fill in the JSON configuration. For more details, visit the [Trae documentation](https://docs.trae.ai/ide/model-context-protocol?_lang=en).

#### Remote Server Connection (Recommended)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "url": "https://hyperfocache.offendingcommit.com/mcp"
    }
  }
}
```

#### Docker-based Connection (Alternative)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

</details>

### Gemini CLI

<details>
<summary><b>Install in Gemini CLI</b></summary>

See [Gemini CLI Configuration](https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/configuration.md) for details.

1. Open the Gemini CLI settings file at `~/.gemini/settings.json`
2. Add the following to the `mcpServers` object:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "httpUrl": "https://hyperfocache.offendingcommit.com/mcp"
    }
  }
}
```

</details>

### BoltAI

<details>
<summary><b>Install in BoltAI</b></summary>

Open the "Settings" page, navigate to "Plugins," and enter:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

More information available on [BoltAI's Documentation site](https://docs.boltai.com/docs/plugins/mcp-servers).

</details>

### Augment Code

<details>
<summary><b>Install in Augment Code</b></summary>

#### Using the Augment Code UI

1. Click the hamburger menu
2. Select **Settings**
3. Navigate to the **Tools** section
4. Click the **+ Add MCP** button
5. Enter the following command:
   ```
   docker run -i --rm -v mcp-auth:/home/mcp/.mcp-auth ghcr.io/offendingcommit/mcp-remote:latest https://hyperfocache.offendingcommit.com/sse
   ```
6. Name the MCP: **HyperFocache**
7. Click the **Add** button

#### Manual Configuration

Add to your `settings.json`:

```json
"augment.advanced": {
  "mcpServers": [
    {
      "name": "hyperfocache",
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  ]
}
```

</details>

### Roo Code

<details>
<summary><b>Install in Roo Code</b></summary>

Add this to your Roo Code MCP configuration file. See [Roo Code MCP docs](https://docs.roocode.com/features/mcp/using-mcp-in-roo) for more info.

#### Remote Server Connection (Recommended)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "type": "streamable-http",
      "url": "https://hyperfocache.offendingcommit.com/mcp"
    }
  }
}
```

#### Docker-based Connection (Alternative)

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

</details>

### Zencoder

<details>
<summary><b>Install in Zencoder</b></summary>

1. Go to the Zencoder menu (...)
2. Select Agent tools
3. Click on Add custom MCP
4. Add the name and configuration:

```json
{
  "command": "docker",
  "args": [
    "run",
    "-i",
    "--rm",
    "-v",
    "mcp-auth:/home/mcp/.mcp-auth",
    "ghcr.io/offendingcommit/mcp-remote:latest",
    "https://hyperfocache.offendingcommit.com/sse"
  ]
}
```

5. Click the Install button

</details>

### Amazon Q Developer CLI

<details>
<summary><b>Install in Amazon Q Developer CLI</b></summary>

Add this to your Amazon Q Developer CLI configuration file. See [Amazon Q Developer CLI docs](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-mcp-configuration.html) for more details.

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

</details>

### Qodo Gen

<details>
<summary><b>Install in Qodo Gen</b></summary>

See [Qodo Gen docs](https://docs.qodo.ai/qodo-documentation/qodo-gen/qodo-gen-chat/agentic-mode/agentic-tools-mcps) for more details.

1. Open Qodo Gen chat panel in VSCode or IntelliJ
2. Click Connect more tools
3. Click + Add new MCP
4. Add the following configuration:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "url": "https://hyperfocache.offendingcommit.com/mcp"
    }
  }
}
```

</details>

### JetBrains AI Assistant

<details>
<summary><b>Install in JetBrains AI Assistant</b></summary>

See [JetBrains AI Assistant Documentation](https://www.jetbrains.com/help/ai-assistant/configure-an-mcp-server.html) for more details.

1. Go to `Settings` -> `Tools` -> `AI Assistant` -> `Model Context Protocol (MCP)`
2. Click `+ Add`
3. Select `As JSON` option
4. Add this configuration:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

5. Click `OK` and then `Apply`

</details>

### Warp

<details>
<summary><b>Install in Warp</b></summary>

See [Warp Model Context Protocol Documentation](https://docs.warp.dev/knowledge-and-collaboration/mcp#adding-an-mcp-server) for details.

1. Navigate `Settings` > `AI` > `Manage MCP servers`
2. Click the `+ Add` button
3. Paste the configuration:

```json
{
  "hyperfocache": {
    "command": "docker",
    "args": [
      "run",
      "-i",
      "--rm",
      "-v",
      "mcp-auth:/home/mcp/.mcp-auth",
      "ghcr.io/offendingcommit/mcp-remote:latest",
      "https://hyperfocache.offendingcommit.com/sse"
    ],
    "env": {},
    "working_directory": null,
    "start_on_launch": true
  }
}
```

4. Click `Save`

</details>

### Opencode

<details>
<summary><b>Install in Opencode</b></summary>

Add this to your Opencode configuration file. See [Opencode MCP docs](https://opencode.ai/docs/mcp-servers) for more info.

#### Remote Server Connection (Recommended)

```json
"mcp": {
  "hyperfocache": {
    "type": "remote",
    "url": "https://hyperfocache.offendingcommit.com/mcp",
    "enabled": true
  }
}
```

#### Docker-based Connection (Alternative)

```json
{
  "mcp": {
    "hyperfocache": {
      "type": "local",
      "command": [
        "docker",
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ],
      "enabled": true
    }
  }
}
```

</details>

### Copilot Coding Agent

<details>
<summary><b>Install in Copilot Coding Agent</b></summary>

Add to your Repository->Settings->Copilot->Coding agent->MCP configuration:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "type": "http",
      "url": "https://hyperfocache.offendingcommit.com/mcp"
    }
  }
}
```

For more information, see the [official GitHub documentation](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/agents/copilot-coding-agent/extending-copilot-coding-agent-with-mcp).

</details>

### Kiro

<details>
<summary><b>Install in Kiro</b></summary>

See [Kiro Model Context Protocol Documentation](https://kiro.dev/docs/mcp/configuration/) for details.

1. Navigate `Kiro` > `MCP Servers`
2. Click the `+ Add` button
3. Paste the configuration:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ],
      "env": {},
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

4. Click `Save`

</details>

### LM Studio

<details>
<summary><b>Install in LM Studio</b></summary>

See [LM Studio MCP Support](https://lmstudio.ai/blog/lmstudio-v0.3.17) for more information.

1. Navigate to `Program` (right side) > `Install` > `Edit mcp.json`
2. Paste the configuration:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ]
    }
  }
}
```

3. Click `Save`
4. Toggle the MCP server on/off from the right side under `Program`

</details>

### Perplexity Desktop

<details>
<summary><b>Install in Perplexity Desktop</b></summary>

See [Local and Remote MCPs for Perplexity](https://www.perplexity.ai/help-center/en/articles/11502712-local-and-remote-mcps-for-perplexity) for more information.

1. Navigate `Perplexity` > `Settings`
2. Select `Connectors`
3. Click `Add Connector`
4. Select `Advanced`
5. Enter Server Name: `HyperFocache`
6. Paste the following JSON:

```json
{
  "command": "docker",
  "args": [
    "run",
    "-i",
    "--rm",
    "-v",
    "mcp-auth:/home/mcp/.mcp-auth",
    "ghcr.io/offendingcommit/mcp-remote:latest",
    "https://hyperfocache.offendingcommit.com/sse"
  ],
  "env": {}
}
```

7. Click `Save`

</details>

### Docker

<details>
<summary><b>Using Docker Directly</b></summary>

If you prefer to run the MCP server in a Docker container without a specific client:

#### Pull and Run the mcp-remote Image

```bash
# Pull the latest image
docker pull ghcr.io/offendingcommit/mcp-remote:latest

# Run with persistent token storage
docker run -it \
  -v mcp-auth:/home/mcp/.mcp-auth \
  ghcr.io/offendingcommit/mcp-remote:latest \
  https://hyperfocache.offendingcommit.com/sse
```

#### Using Docker Compose

Create a `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  hyperfocache:
    image: ghcr.io/offendingcommit/mcp-remote:latest
    container_name: hyperfocache
    volumes:
      - mcp-auth:/home/mcp/.mcp-auth
    ports:
      - "3334:3334"  # For OAuth callback if needed
    command: ["https://hyperfocache.offendingcommit.com/sse"]
    restart: unless-stopped

volumes:
  mcp-auth:
    driver: local
```

Run with: `docker-compose up`

#### Building from Source

```bash
# Clone the mcp-remote repository
git clone https://github.com/offendingcommit/mcp-remote.git
cd mcp-remote

# Build the image
docker build -t mcp-remote:local .

# Run HyperFocache
docker run -it \
  -v mcp-auth:/home/mcp/.mcp-auth \
  mcp-remote:local \
  https://hyperfocache.offendingcommit.com/sse
```

</details>

### Windows

<details>
<summary><b>Install on Windows</b></summary>

For Windows users, the configuration differs slightly from Linux/macOS. Here's an example using Cline:

```json
{
  "mcpServers": {
    "hyperfocache": {
      "command": "cmd",
      "args": [
        "/c",
        "docker",
        "run",
        "-i",
        "--rm",
        "-v",
        "mcp-auth:/home/mcp/.mcp-auth",
        "ghcr.io/offendingcommit/mcp-remote:latest",
        "https://hyperfocache.offendingcommit.com/sse"
      ],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Make sure Docker Desktop for Windows is installed and running before using the configuration.

</details>

## Feedback & Support

We value your input and want to make HyperFocache better for everyone!

### 📝 Submit Feedback
**Google Form**: [https://forms.gle/rPSh6xeeSUbngAbu7](https://forms.gle/rPSh6xeeSUbngAbu7)
- Feature requests
- Bug reports
- UX/UI feedback
- General suggestions

### 🐛 Report Issues
For technical issues, bugs, or feature requests, please use our feedback form above. We're actively monitoring all submissions and prioritize based on community needs.

### 💡 Suggestions Welcome
- Workflow improvements
- Integration ideas
- Performance optimizations
- Accessibility enhancements

### 🤝 Community
Join our growing community of developers using HyperFocache to amplify their cognitive abilities. Your experiences and insights help shape the future of the project.

## Getting Started

Visit [hyperfocache.com](https://hyperfocache.com) to begin using HyperFocache with your GitHub account.

## About

HyperFocache combines neural network concepts with cache memory blocks, creating a modern tech-forward solution for cognitive augmentation. It's not just a tool - it's your external brain, designed to work the way your mind does.

---

*Built with ❤️ for the ADHD developer community*