# AWS MCP: Model Context Protocol on AWS

[![GitHub Stars](https://img.shields.io/github/stars/ihatesea69/AWS-MCP?style=social)](https://github.com/ihatesea69/AWS-MCP)
[![GitHub Forks](https://img.shields.io/github/forks/ihatesea69/AWS-MCP?style=social)](https://github.com/ihatesea69/AWS-MCP/fork)
[![GitHub Issues](https://img.shields.io/github/issues/ihatesea69/AWS-MCP)](https://github.com/ihatesea69/AWS-MCP/issues)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green?logo=node.js)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue?logo=typescript)](https://www.typescriptlang.org/)

## Introduction to Model Context Protocol (MCP)

### Getting Started with MCP

MCP (Model Context Protocol) is an open protocol that standardizes how applications provide context to large language models (LLMs). Think of MCP like a USB-C port for AI applications. Just as USB-C provides a standard method for connecting devices to various accessories, MCP provides a standard method for connecting AI models to different data sources and tools.

### Why Use MCP?

MCP enables building complex agents and automated workflows based on LLMs. LLMs often need to integrate with data and tools, and MCP provides:

- **A growing list of ready-to-use integrations** that allow your LLM to connect directly.
- **Flexibility** to switch between LLM providers.
- **Best data security practices** within your infrastructure.

### General Architecture

At its core, MCP follows a client-server architecture where a host application can connect to multiple servers:

- **MCP Hosts**: Programs like Claude Desktop, IDEs, or AI tools that want to access data through MCP.
- **MCP Clients**: Protocol clients that maintain 1:1 connections with servers.
- **MCP Servers**: Lightweight programs, each providing specific capabilities through the Model Context Protocol.
- **Local Data Sources**: Files, databases, and services on your computer that MCP servers can securely access.
- **Remote Services**: External systems available on the Internet (e.g., via APIs) that MCP servers can connect to.

---

## Introduction to AWS MCP

AWS MCP (Model Context Protocol) is a server that enables AI assistants like Claude to interact with AWS environments through natural language. This makes it easy to manage and query AWS resources without using the traditional AWS Console or CLI.

AWS MCP can be considered a powerful alternative to Amazon Q, offering greater flexibility and security.

## Key Features

- **Query and modify AWS resources using natural language**
- **Support for multiple AWS profiles and SSO authentication**
- **Multi-region AWS support**
- **Secure credential management** (credentials are never exposed externally, only used locally)
- **Local execution with your AWS credentials**

## Prerequisites

To use AWS MCP, ensure your environment has:

- **Node.js**
- **Claude Desktop application**
- **Locally configured AWS credentials (AWS Configure)** (stored in `~/.aws/`)

## Installation Guide

### 1. Clone the repository

First, download the source code from GitHub to your computer:

```bash
git clone https://github.com/ihatesea69/AWS-MCP
cd aws-mcp
```

### 2. Install dependencies

You can use `pnpm` or `npm` to install:

```bash
pnpm install
# or
npm install
```

## Configuration and Usage with Claude Desktop

### 1. Configure in Claude Desktop

Open the Claude Desktop application and navigate to:

```
Settings -> Developer -> Edit Config
```

Then add the following entry to the `claude_desktop_config.json` file:

```json
{
  "mcpServers": {
    "aws": {
      "command": "npm", // or pnpm
      "args": [
        "--silent",
        "--prefix",
        "/Users/<YOUR USERNAME>/aws-mcp",
        "start"
      ]
    }
  }
}
```

> Note: Replace `/Users/<YOUR USERNAME>/aws-mcp` with the actual path to your project directory.

### 2. Restart Claude Desktop

Run your project by navigating (cd) to the directory containing index.ts and running the NPM start command.

After editing the configuration, restart the Claude Desktop application. If the installation is correct, you will see a successful connection message with MCP.

### 3. Using AWS MCP in Claude

You can start using it by entering natural language commands such as:

- "List available AWS profiles"
- "List all EC2 instances in my account"
- "Show me S3 buckets with their sizes"
- "What Lambda functions are deployed in us-east-1?"
- "List all ECS clusters and their services"

## Configuration with `nvm`

If you use Node.js through `nvm`, compile from source first and add the following configuration:

```json
{
  "mcpServers": {
    "aws": {
      "command": "/Users/<USERNAME>/.nvm/versions/node/v20.10.0/bin/node",
      "args": [
        "<WORKSPACE_PATH>/aws-mcp/node_modules/tsx/dist/cli.mjs",
        "<WORKSPACE_PATH>/aws-mcp/index.ts",
        "--prefix",
        "<WORKSPACE_PATH>/aws-mcp",
        "start"
      ]
    }
  }
}
```

> Note: Replace `<USERNAME>` and `<WORKSPACE_PATH>` with the actual paths on your system.

## Conclusion

AWS MCP is a powerful tool that allows you to manage AWS resources using the Claude AI assistant. With the ability to query and control through natural language, AWS MCP significantly simplifies AWS management. If you are looking for an alternative to Amazon Q, AWS MCP is a worthy consideration!

## Credits

Original source: https://github.com/RafalWilinski/aws-mcp
