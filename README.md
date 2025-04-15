# Memory MCP Server (Go)

> A Model Context Protocol server that provides knowledge graph management capabilities. This server enables LLMs to create, read, update, and delete entities and relations in a persistent knowledge graph, helping AI assistants maintain memory across conversations. This is a Go implementation of the official [TypeScript Memory MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/memory).

![Go Platform](https://img.shields.io/badge/platform-cross--platform-lightgrey)
![License](https://img.shields.io/badge/license-MIT-blue)

## ✨ Features

* **Knowledge Graph Storage**: Maintain a persistent graph of entities and their relationships
* **Entity Management**: Create, retrieve, update, and delete entities with custom types
* **Relation Tracking**: Define and manage relationships between entities in active voice
* **Observation System**: Add and remove observations about entities over time
* **Powerful Search**: Find relevant nodes by name, type, or observation content
* **Persistent Storage**: Data persists between sessions in a simple JSON format
* **Flexible Transport Modes**: Supports both stdio (standard input/output) and SSE (Server-Sent Events) transport modes
* **Cross-Platform**: Works on Linux, macOS, and Windows

## Available Tools

* `create_entities` - Create multiple new entities in the knowledge graph
  * `entities` (array, required): Array of entity objects to create
    * `name` (string): The name of the entity
    * `entityType` (string): The type of the entity
    * `observations` (array of strings): Observations associated with the entity

* `create_relations` - Create multiple new relations between entities
  * `relations` (array, required): Array of relation objects
    * `from` (string): The name of the entity where the relation starts
    * `to` (string): The name of the entity where the relation ends
    * `relationType` (string): The type of the relation (in active voice)

* `add_observations` - Add new observations to existing entities
  * `observations` (array, required): Array of observation additions
    * `entityName` (string): The name of the entity to add observations to
    * `contents` (array of strings): The observations to add

* `delete_entities` - Delete multiple entities and their associated relations
  * `entityNames` (array, required): Array of entity names to delete

* `delete_observations` - Delete specific observations from entities
  * `deletions` (array, required): Array of observation deletions
    * `entityName` (string): The name of the entity containing the observations
    * `observations` (array of strings): The observations to delete

* `delete_relations` - Delete multiple relations from the knowledge graph
  * `relations` (array, required): Array of relation objects to delete
    * `from` (string): The source entity name
    * `to` (string): The target entity name
    * `relationType` (string): The relation type

* `read_graph` - Read the entire knowledge graph
  * No parameters required

* `search_nodes` - Search for nodes in the knowledge graph based on a query
  * `query` (string, required): Search query to match against entity names, types, and observations

* `open_nodes` - Open specific nodes in the knowledge graph by their names
  * `names` (array, required): Array of entity names to retrieve

## Installation

### Option 1: Download Pre-built Binary

Download the latest pre-built binary for your platform from the [GitHub Releases](https://github.com/okooo5km/memory-mcp-server-go/releases/latest) page:

Download the binary for your platform from the [GitHub Releases](https://github.com/okooo5km/memory-mcp-server-go/releases/latest) page and follow the installation instructions below.

<details>
<summary><b>macOS Installation</b></summary>

#### macOS with Apple Silicon (M1/M2/M3):
```bash
# Download the arm64 version
curl -L https://github.com/okooo5km/memory-mcp-server-go/releases/latest/download/memory-mcp-server-go-macos-arm64.zip -o memory-mcp-server.zip
unzip memory-mcp-server.zip
chmod +x memory-mcp-server-go

# Install to your local bin directory
mkdir -p ~/.local/bin
mv memory-mcp-server-go ~/.local/bin/
rm memory-mcp-server.zip
```

#### macOS with Intel Processor:
```bash
# Download the x86_64 version
curl -L https://github.com/okooo5km/memory-mcp-server-go/releases/latest/download/memory-mcp-server-go-macos-x86_64.zip -o memory-mcp-server.zip
unzip memory-mcp-server.zip
chmod +x memory-mcp-server-go

# Install to your local bin directory
mkdir -p ~/.local/bin
mv memory-mcp-server-go ~/.local/bin/
rm memory-mcp-server.zip
```

#### macOS Universal Binary (works on both Apple Silicon and Intel):
```bash
# Download the universal version
curl -L https://github.com/okooo5km/memory-mcp-server-go/releases/latest/download/memory-mcp-server-go-macos-universal.zip -o memory-mcp-server.zip
unzip memory-mcp-server.zip
chmod +x memory-mcp-server-go

# Install to your local bin directory
mkdir -p ~/.local/bin
mv memory-mcp-server-go ~/.local/bin/
rm memory-mcp-server.zip
```
</details>

<details>
<summary><b>Linux Installation</b></summary>

#### Linux on x86_64 (most common):
```bash
# Download the amd64 version
curl -L https://github.com/okooo5km/memory-mcp-server-go/releases/latest/download/memory-mcp-server-go-linux-amd64.tar.gz -o memory-mcp-server.tar.gz
tar -xzf memory-mcp-server.tar.gz
chmod +x memory-mcp-server-go

# Install to your local bin directory
mkdir -p ~/.local/bin
mv memory-mcp-server-go ~/.local/bin/
rm memory-mcp-server.tar.gz
```

#### Linux on ARM64 (e.g., Raspberry Pi 4, AWS Graviton):
```bash
# Download the arm64 version
curl -L https://github.com/okooo5km/memory-mcp-server-go/releases/latest/download/memory-mcp-server-go-linux-arm64.tar.gz -o memory-mcp-server.tar.gz
tar -xzf memory-mcp-server.tar.gz
chmod +x memory-mcp-server-go

# Install to your local bin directory
mkdir -p ~/.local/bin
mv memory-mcp-server-go ~/.local/bin/
rm memory-mcp-server.tar.gz
```
</details>

<details>
<summary><b>Windows Installation</b></summary>

#### Windows on x86_64 (most common):
- Download the [Windows AMD64 version](https://github.com/okooo5km/memory-mcp-server-go/releases/latest/download/memory-mcp-server-go-windows-amd64.zip)
- Extract the ZIP file
- Move the `memory-mcp-server-go.exe` to a location in your PATH

#### Windows on ARM64 (e.g., Windows on ARM devices):
- Download the [Windows ARM64 version](https://github.com/okooo5km/memory-mcp-server-go/releases/latest/download/memory-mcp-server-go-windows-arm64.zip)
- Extract the ZIP file
- Move the `memory-mcp-server-go.exe` to a location in your PATH
</details>

Make sure the installation directory is in your PATH:

- **macOS/Linux**: Add `export PATH="$HOME/.local/bin:$PATH"` to your shell configuration file (`.bashrc`, `.zshrc`, etc.)
- **Windows**: Add the directory to your system PATH through the System Properties > Environment Variables dialog

### Option 2: Build from Source

1. Clone the repository:

   ```bash
   git clone https://github.com/okooo5km/memory-mcp-server-go.git
   cd memory-mcp-server-go
   ```

2. Build the project:

   **Using Make (recommended):**
   ```bash
   # Build for your current platform
   make
   
   # Or build for a specific platform
   make build-darwin-universal    # macOS Universal Binary
   make build-darwin-arm64        # macOS Apple Silicon
   make build-darwin-amd64        # macOS Intel
   make build-linux-amd64         # Linux x86_64
   make build-linux-arm64         # Linux ARM64
   make build-windows-amd64       # Windows x86_64
   
   # Or build for all platforms at once
   make build-all
   
   # Create distribution packages for all platforms
   make dist
   ```
   
   The binaries will be placed in the `.build` directory.

   **Using Go directly:**
   ```bash
   go build
   ```

3. Install the binary:

   ```bash
   # Install to user directory (recommended, no sudo required)
   mkdir -p ~/.local/bin
   cp memory-mcp-server-go ~/.local/bin/
   ```

   Make sure `~/.local/bin` is in your PATH by adding to your shell configuration file:

   ```bash
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc  # or ~/.bashrc
   source ~/.zshrc  # or source ~/.bashrc
   ```

## Command Line Arguments

The server supports the following command line arguments:

* `-t, --transport`: Specify the transport type (stdio or sse, defaults to stdio)
* `-m, --memory`: Custom path for storing the knowledge graph (optional)
* `-p, --port`: Port number for SSE transport (defaults to 8080)

Example usage:

```bash
# Use default settings (stdio transport, default memory file)
memory-mcp-server-go

# Specify a custom memory file location
memory-mcp-server-go --memory /path/to/your/memory.json

# Use SSE transport on a specific port
memory-mcp-server-go --transport sse --port 9000
```

## Memory File Storage Path

The `memory.json` file is used to store the knowledge graph data. The server determines its location using the following priority rules:

1. Command line argument: If you provide a path with the `-m` or `--memory` flag, this path will be used
2. Environment variable: If no command line argument is provided, the server checks for the `MEMORY_FILE_PATH` environment variable
3. Default location: If neither of the above is specified, the server defaults to `memory.json` in the same directory as the executable

Path handling rules:
* If you provide an absolute path (e.g., `/home/user/data/memory.json` or `C:\Users\user\data\memory.json`), it will be used as-is
* If you provide a relative path (e.g., `custom/memory.json`), it will be resolved relative to the executable's directory

For example, if your executable is located at `/usr/local/bin/memory-mcp-server-go`, and you don't specify any path, the default file path will be `/usr/local/bin/memory.json`. If you specify a relative path like `custom/memory.json`, the actual file path will be `/usr/local/bin/custom/memory.json`.

## Configuration

### Configure for Claude.app

Add to your Claude settings:

```json
"mcpServers": {
  "memory": {
    "command": "memory-mcp-server-go",
    "env": {
      "MEMORY_FILE_PATH": "/Path/Of/Your/memory.json"
    }
  }
}
```

### Configure for Cursor

Add the following configuration to your Cursor editor's Settings - mcp.json:

```json
{
  "mcpServers": {
    "memory": {
      "command": "memory-mcp-server-go",
      "env": {
        "MEMORY_FILE_PATH": "/Path/Of/Your/memory.json"
      }
    }
  }
}
```

### Example System Prompt

You can use the following system prompt to help Claude utilize the memory-mcp-server effectively:

```
You have access to a Knowledge Graph memory system, which can store and retrieve information across conversations. Use it to remember important details about the user, their preferences, and any facts they've shared.

When you discover important information, save it using memory tools:
- `create_entities` to add new people, places, or concepts
- `create_relations` to record how entities relate to each other
- `add_observations` to record facts about existing entities

Before answering questions that might require past context, check your memory:
- `search_nodes` to find relevant information
- `open_nodes` to retrieve specific entities
- `read_graph` to get a complete view of your knowledge

Always prioritize information from your memory when responding to the user, especially when they reference past conversations.
```

## Development Requirements

* Go 1.20 or later
* github.com/mark3labs/mcp-go

## Knowledge Graph Structure

The Memory MCP Server uses a simple graph structure to store knowledge:

* **Entities**: Nodes in the graph with a name, type, and list of observations
* **Relations**: Edges between entities with a relation type in active voice
* **Observations**: Facts or details associated with entities

The knowledge graph is persisted to disk as a line-delimited JSON file, where each line is either an entity or relation object.

## Usage Examples

### Creating Entities

```json
{
  "entities": [
    {
      "name": "John Smith",
      "entityType": "Person",
      "observations": ["Software engineer", "Lives in San Francisco", "Enjoys hiking"]
    },
    {
      "name": "Acme Corp",
      "entityType": "Company",
      "observations": ["Founded in 2010", "Tech startup"]
    }
  ]
}
```

### Creating Relations

```json
{
  "relations": [
    {
      "from": "John Smith",
      "to": "Acme Corp",
      "relationType": "works at"
    }
  ]
}
```

### Adding Observations

```json
{
  "observations": [
    {
      "entityName": "John Smith",
      "contents": ["Recently promoted to Senior Engineer", "Working on AI projects"]
    }
  ]
}
```

### Searching Nodes

```json
{
  "query": "San Francisco"
}
```

### Opening Specific Nodes

```json
{
  "names": ["John Smith", "Acme Corp"]
}
```

## Use Cases

* **Long-term Memory for AI Assistants**: Enable AI assistants to remember user preferences, past interactions, and important facts
* **Knowledge Management**: Organize information about people, places, events, and concepts
* **Relationship Tracking**: Maintain networks of relationships between entities
* **Context Persistence**: Preserve important context across multiple sessions
* **Journal and Daily Logs**: Maintain a structured record of events, activities, and reflections over time, making it easy to retrieve and relate past experiences chronologically

## Version History

See GitHub Releases for version history and changelog.

## License

memory-mcp-server-go is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License.

## About

A Go implementation of a knowledge graph memory server for Model Context Protocol (MCP), enabling persistent memory capabilities for large language models. This project is based on the [official TypeScript implementation](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) but rewritten in Go using the MCP Go SDK.
