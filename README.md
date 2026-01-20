***

# Gemini-cli-MCP

**Gemini CLI MCP server** — A powerful, terminal-first interface for interacting with Google's Gemini models, featuring built-in tools and Model Context Protocol (MCP) support.

## 🚀 Why Gemini CLI?

*   **🎯 Free tier:** 60 requests/min and 1,000 requests/day with a personal Google account.
*   **🧠 Powerful Gemini 3 models:** Access to improved reasoning and a 1M token context window.
*   **🔧 Built-in tools:** Google Search grounding, file operations, shell commands, and web fetching.
*   **🔌 Extensible:** MCP support for custom integrations.
*   **💻 Terminal-first:** Designed for developers who live in the command line.
*   **🛡️ Open source:** Apache 2.0 licensed.

---

## 📦 Installation

### Pre-requisites
*   **Node.js**: version 20 or higher
*   **OS**: macOS, Linux, or Windows

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

---

## 🔐 Authentication Options

Choose the authentication method that best fits your needs:

### OPtion 1: Login with Google (OAuth)
**Best for:** Individual developers and Gemini Code Assist License holders.

*   **Benefits:** Free tier (60 req/min), 1M token context, no API key management.
*   **Setup:** Simply start the CLI and follow the browser prompt.
    ```bash
    gemini
    ```
*   *Note: If using a paid Code Assist License, set your project ID:*
    ```bash
    export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"
    gemini
    ```

### Option 2: Gemini API Key
**Best for:** Developers needing specific model control or paid tier access.

*   **Benefits:** 1,000 requests/day, specific model selection, usage-based billing.
*   **Setup:** Get your key from [Google AI Studio](https://aistudio.google.com/apikey).
    ```bash
    export GEMINI_API_KEY="YOUR_API_KEY"
    gemini
    ```

### Option 3: Vertex AI
**Best for:** Enterprise teams and production workloads.

*   **Benefits:** Advanced security, compliance, and higher rate limits.
*   **Setup:**
    ```bash
    export GOOGLE_API_KEY="YOUR_API_KEY"
    export GOOGLE_GENAI_USE_VERTEXAI=true
    gemini
    ```

---

## 🚀 Getting Started

### Basic Usage
Start the CLI in your current directory:
```bash
gemini
```

Use a specific model:
```bash
gemini -m gemini-2.5-flash
```

### Quick Examples

**Start a new project:**
```bash
cd new-project/
gemini
```

**Analyze existing code:**
```bash
git clone https://github.com/google-gemini/gemini-cli
cd gemini-cli
gemini
# Inside the prompt:
> Give me a summary of all of the changes that went in yesterday
```

---






To help you integrate this into your documentation, I have formatted the "MCP Server for Network Engineers" content into a structured Lab Guide format. This can be added as a separate section or a standalone `LAB.md` file.

### Reasoning for the Structure:
1.  **Lab Overview**: Clearly states the learning objective.
2.  **Prerequisites**: Ensures the user has the necessary background and tools before starting.
3.  **Step-by-Step Tasks**: Breaks down the installation and configuration into logical phases.
4.  **Practical Examples**: Includes sample prompts to help the user immediately test the integration.

***

This is a comprehensive and structured README for your GitHub repository, designed specifically for the **MCP Server for Network Engineers** lab. It follows a logical flow from prerequisites to final configuration.

***

# 🛠️ Lab: MCP Server for Network Engineers

## 📖 Description
By the end of this lab, students will understand how to use an **MCP (Model Context Protocol) Server** to connect to Network Devices and interact with them using AI-driven prompts. This lab bridges the gap between Large Language Models (LLMs) and physical/virtual network infrastructure.

## 🗓️ Agenda
1.  **Environment Setup**: Install the MCP client and MCP Server on your local machine.
2.  **Integration**: Connect the MCP Server with the MCP Client (Gemini CLI).
3.  **Validation**: Test the interaction between the LLM and external network devices (Linux Server or ASR9K).

## ⚙️ Pre-requisites
*   **AI Fundamentals**: Basic understanding of Generative AI and Prompt Engineering.
*   **MCP Knowledge**: Familiarity with the Model Context Protocol concept.
*   **Technical Skills**: Experience working with the macOS Terminal or Windows Command Prompt.
*   **Hardware**: A laptop with administrative privileges.

---

## 🚀 Step-by-Step Environment Setup

### 1. Install Package Managers
Package managers allow you to easily install and update software from the command line.

*   **Windows (winget):**
    Ensure `winget` is installed.
     ```bash
    https://learn.microsoft.com/en-us/windows/package-manager/winget/
    ```
*   **macOS/Linux (Homebrew):**
    Open your terminal and run:
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

### 2. Install `uv`
`uv` is an extremely fast Python package and project manager used to run the MCP Server.

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

### 4. Install Build Tools
*   **Windows:**
    ```cmd
    winget install -e --id Microsoft.VisualStudio.2022.BuildTools
    ```
*   **macOS/Linux:**
    ```bash
    No action required (built into the OS).
    ```



### 5. Configure and Run Netmiko MCP Server
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

:: Fetch sample device configuration
curl -LJO https://wwwin-github.cisco.com/raw/nipc/CX-Lighhouse-AI-Labs/refs/heads/MCP-Server-for-Network-Engineers/my-devices.network.toml

:: Test the server (Exit with Ctrl+C if a blank screen appears)
uv run --python 3.13.9 --with "mcp[cli]" --with netmiko main.py my-devices.network.toml
```

### 6. Verify `uv` Path
You will need the exact path for the next step.
*   **Windows:** `where uv`
*   **macOS/Linux:** `which uv`

### 7. The Gemini CLI uses the `mcpServers` configuration in your `settings.json` file to locate and connect to MCP servers. This configuration supports multiple servers with different transport          mechanisms.
###    You can configure MCP servers in your `settings.json` file in two main ways: through the top-level `mcpServers` object for specific server definitions, and through the `mcp` object for             global settings that control server discovery and execution.

### 7. Integrate with Gemini CLI
1.  Open terminal
2.  Go to home directory `cd ~ `.
3.  Go to the folder `cd .gemini` which should already be present if you have installed Gemini CLI from earlier steps.
4.  You can open the foldersettings.json in VS code with `code .\settings.json`.
5.  Add the JSON configuration after whatever present in the settings.json file with new comma. **Replace the bold placeholders** with your actual system username and `uv` path.

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
      "command": "C:/Users/YOUR_USERNAME/.local/bin/uv.exe",
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
        "/Users/YOUR_USERNAME/git/mcp-netmiko-server",
        "main.py",
        "my-devices.network.toml"
      ]
    }
  }
}
```

### 8. Finalize
*   **Windows**: Restart your VS code or commadn prompt.
*   **macOS**: Restart the VS code or command prompt to reload the configuration.

---

## 🧪 Verify the installation of MCP
* After all the chnages you will see 1 MCP server when you start Gemini again.
<img width="1771" height="145" alt="image" src="https://github.com/user-attachments/assets/12b2642b-8fe5-4d93-9591-dea85a3ac0fe" />

* You can check MCP related command with `/mcp`.
<img width="1920" height="382" alt="image" src="https://github.com/user-attachments/assets/e8e6a1d9-8ee9-4c57-853f-7cc454ebb81d" />

## Testing your integration
* You can start with `/mcp list?`
  <img width="1938" height="259" alt="image" src="https://github.com/user-attachments/assets/d0e4ab65-68e2-4eb8-bc1d-898480960519" />

* It will show you the list of MCP servers.
<img width="1991" height="456" alt="image" src="https://github.com/user-attachments/assets/f7b34f79-49b6-4328-901b-6f89ceb88723" />





---

 
