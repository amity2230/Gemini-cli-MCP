
***

# Gemini CLI & MCP Server Lab

**Gemini CLI MCP server** — A powerful, terminal-first interface for interacting with Google's Gemini models, featuring built-in tools and Model Context Protocol (MCP) support.

This repository guides you through installing the Gemini CLI and configuring a **Network Device MCP Server** (using Netmiko) to bridge the gap between LLMs and physical/virtual network infrastructure.

---

## 🚀 Why Gemini CLI?

*   **🎯 Free tier:** 60 requests/min and 1,000 requests/day with a personal Google account.
*   **🧠 Powerful Gemini 3 models:** Access to improved reasoning and a 1M token context window.
*   **🔧 Built-in tools:** Google Search grounding, file operations, shell commands, and web fetching.
*   **🔌 Extensible:** MCP support for custom integrations.
*   **💻 Terminal-first:** Designed for developers who live in the command line.
*   **🛡️ Open source:** Apache 2.0 licensed.

---

## 📖 Lab Overview

By the end of this lab, you will understand how to use an **MCP (Model Context Protocol) Server** to connect to Network Devices and interact with them using AI-driven prompts.

### Agenda
1.  **Gemini CLI Setup**: Install and authenticate the base CLI tool.
2.  **Environment Setup**: Install dependencies (`uv`, `git`) for the MCP server.
3.  **Integration**: Connect the Netmiko MCP Server with the Gemini CLI.
4.  **Validation**: Test the interaction between the LLM and external network devices.

---

## Part 1: Gemini CLI Installation

### Pre-requisites
*   **Node.js**: Version 20 or higher ([Download](https://nodejs.org/en/download)).
*   **OS**: macOS, Linux, or Windows.

### Quick Install
Choose one of the following methods:

**Using npx (No installation required)**
```bash
npx @google/gemini-cli
```

**Using npm (Global installation)**
```bash
npm install -g @google/gemini-cli
```

**Using Homebrew (macOS/Linux)**
```bash
brew install gemini-cli
```

### Authentication
Choose the method that fits your needs:

**Option 1: Login with Google (OAuth) - *Recommended for Individuals***
Simply start the CLI and follow the browser prompt.
```bash
gemini
```

**Option 2: Gemini API Key**
Get your key from [Google AI Studio](https://aistudio.google.com/apikey).
```bash
export GEMINI_API_KEY="YOUR_API_KEY"
gemini
```

---

## Part 2: MCP Server Environment Setup

### 1. Install Package Managers
*   **Windows:** Ensure `winget` is installed ([Learn more](https://learn.microsoft.com/en-us/windows/package-manager/winget/)).
*   **macOS/Linux:** Install Homebrew:
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

### 2. Install `uv`
`uv` is a fast Python package manager used to run the MCP Server.

*   **Windows:**
    ```cmd
    winget install --id=astral-sh.uv -e
    ```
*   **macOS/Linux:**
    ```bash
    brew install uv
    ```

### 3. Install Git
*   **Windows:**
    ```cmd
    winget install --id Git.Git -e --source winget
    ```
*   **macOS/Linux:**
    ```bash
    brew install git
    ```

> [!IMPORTANT]
> **Restart your terminal** after this step to ensure `uv` and `git` commands are available in your path.

### 4. Install Build Tools (Windows Only)
*   **Windows:**
    ```cmd
    winget install -e --id Microsoft.VisualStudio.2022.BuildTools
    ```

---

## Part 3: Configure Netmiko MCP Server

### 1. Clone and Test Server
Clone the repository and verify the server can run locally.

**Windows:**
```cmd
:: Run as Administrator
mkdir C:\git
cd C:\git
git clone https://github.com/upa/mcp-netmiko-server
cd mcp-netmiko-server

:: Fetch sample device configuration
curl -LJO https://wwwin-github.cisco.com/raw/nipc/CX-Lighhouse-AI-Labs/refs/heads/MCP-Server-for-Network-Engineers/my-devices.network.toml

:: Test the server (Exit with Ctrl+C if a blank screen appears)
uv run --python 3.13.9 --with "mcp[cli]" --with netmiko main.py my-devices.network.toml
```

**macOS/Linux:**
```bash
mkdir ~/git
cd ~/git
git clone https://github.com/upa/mcp-netmiko-server
cd mcp-netmiko-server

# Fetch sample device configuration
curl -LJO https://wwwin-github.cisco.com/raw/nipc/CX-Lighhouse-AI-Labs/refs/heads/MCP-Server-for-Network-Engineers/my-devices.network.toml

# Test the server (Exit with Ctrl+C if a blank screen appears)
uv run --python 3.13.9 --with "mcp[cli]" --with netmiko main.py my-devices.network.toml
```

### 2. Locate `uv` Path
Run the following to find your path (needed for the next step):
*   **Windows:** `where uv`
*   **macOS/Linux:** `which uv`

### 3. Integrate with Gemini CLI
The Gemini CLI uses `settings.json` to locate MCP servers.

1.  Open your terminal.
2.  Navigate to the Gemini configuration folder: `cd ~/.gemini` (or `cd %USERPROFILE%\.gemini` on Windows).
3.  Open `settings.json` (e.g., `code settings.json`).
4.  Add the `mcpServers` configuration block.

**⚠️ Note:** Add the JSON configuration after whatever present in the settings.json file with new comma. **Replace the ** **amit** ** placeholders** with your actual system username and `uv` path.

**Windows Configuration:**
```json
{
  "ide": {
    "hasSeenNudge": true
  },
  "security": {
    "auth": {
      "selectedType": "oauth-personal"
    }
  },
  "mcpServers": {
    "netmiko server": {
      "command": "C:/Users/**amit**/.local/bin/uv.exe",
      "args": [
        "run",
        "--python",
        "3.13.9",
        "--with",
        "mcp[cli]",
        "--with",
        "netmiko",
        "--directory",
        "C:/git/mcp-netmiko-server",
        "main.py",
        "my-devices.network.toml"
      ]
    }
  }
}
```

**macOS Configuration:**
```json
{
  "ide": {
    "hasSeenNudge": true
  },
  "security": {
    "auth": {
      "selectedType": "oauth-personal"
    }
  },
  "mcpServers": {
    "netmiko server": {
      "command": "/opt/homebrew/bin/uv",
      "args": [
        "run",
        "--python",
        "3.13.9",
        "--with",
        "mcp[cli]",
        "--with",
        "netmiko",
        "--directory",
        "/Users/**amit**/git/mcp-netmiko-server",
        "main.py",
        "my-devices.network.toml"
      ]
    }
  }
}
```

### 4. Finalize
Restart your terminal or VS Code to reload the configuration.

---

## 🧪 Verification & Testing

### Verify MCP Installation
Start the Gemini CLI. You should see "1 MCP server" listed in the startup logs.
```bash
gemini
```
*(Example output: `MCP Servers: 1 connected`)*

### Test Commands
Inside the Gemini prompt, use the following commands:

1.  **Check MCP status:**
    ```text
    /mcp
    ```
    <img width="1920" height="382" alt="Screenshot 2026-01-21 003111" src="https://github.com/user-attachments/assets/b9448f3d-dd6c-42cf-a2c8-528a3d6970e5" />

2.  **List available tools:**
    ```text
    /mcp list
    ```
    *This will display the list of tools provided by the Netmiko server.*
    <img width="1938" height="259" alt="Screenshot 2026-01-21 003431" src="https://github.com/user-attachments/assets/ff4d4c95-e067-4d0f-ab4c-fe4f60b66f0d" />
    <img width="1991" height="456" alt="Screenshot 2026-01-21 003511" src="https://github.com/user-attachments/assets/a84396ac-c11b-4299-91dd-9f41def5358d" />



4.  **Interact with the server (Example Prompt):**
    ```text
    > Connect to the router defined in my-devices and show me the running configuration.
    ```  
 
