# GREB MCP Server

Semantic code search for AI agents. Search your codebase using natural language queries.

[![npm version](https://img.shields.io/npm/v/cheetah-greb.svg)](https://www.npmjs.com/package/cheetah-greb)
[![PyPI version](https://img.shields.io/pypi/v/cheetah-greb.svg)](https://pypi.org/project/cheetah-greb/)

## Features

- **Natural Language Search** - Describe what you're looking for in plain English
- **High-Precision Results** - Smart ranking returns the most relevant code first
- **Works with Any MCP Client** - Claude Desktop, Cursor, Windsurf, Cline, Kiro, and more
- **No Indexing Required** - Search any codebase instantly without setup
- **Fast** - Results in under 5 seconds even for large repositories

## Installation

Install Greb globally using pip or npm:

**Python:**

```bash
pip install cheetah-greb
```

**Node.js:**

```bash
npm install -g cheetah-greb
```

## Get Your API Key

1. Go to [Dashboard → API Keys](https://grebmcp.com/dashboard/api-keys)
2. Click **Create API Key**
3. Copy the key (starts with `grb_`)

## Configuration

Add to your MCP client config (Cursor, Windsurf, Claude Desktop, Kiro, etc.):

**Python installation:**

```json
{
  "mcpServers": {
    "greb-mcp": {
      "command": "greb-mcp",
      "env": {
        "GREB_API_KEY": "grb_your_api_key_here"
      }
    }
  }
}
```

**Node.js installation:**

```json
{
  "mcpServers": {
    "greb-mcp": {
      "command": "greb-mcp-js",
      "env": {
        "GREB_API_KEY": "grb_your_api_key_here"
      }
    }
  }
}
```

## Claude Code Setup

**Mac/Linux (Python):**

```bash
claude mcp add --transport stdio greb-mcp --env GREB_API_KEY=grb_your_api_key_here -- greb-mcp
```

**Windows PowerShell (Python):**

```bash
claude mcp add greb-mcp greb-mcp --transport stdio --env "GREB_API_KEY=grb_your_api_key_here"
```

**Mac/Linux (Node.js):**

```bash
claude mcp add --transport stdio greb-mcp --env GREB_API_KEY=grb_your_api_key_here -- greb-mcp-js
```

**Windows PowerShell (Node.js):**

```bash
claude mcp add greb-mcp greb-mcp-js --transport stdio --env "GREB_API_KEY=grb_your_api_key_here"
```

## Tool: `code_search`

Search code using natural language queries powered by AI.

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `query` | string | Yes | Natural language search query |
| `keywords` | object | Yes | Search configuration |
| `keywords.primary_terms` | string[] | Yes | High-level semantic terms (e.g., "authentication", "database") |
| `keywords.code_patterns` | string[] | No | Literal code patterns to grep for |
| `keywords.file_patterns` | string[] | Yes | File extensions to search (e.g., `["*.ts", "*.js"]`) |
| `keywords.intent` | string | Yes | Brief description of what you're looking for |
| `directory` | string | Yes | **Full absolute path** to directory to search |

### Example

```json
{
  "query": "find authentication middleware",
  "keywords": {
    "primary_terms": ["authentication", "middleware", "jwt"],
    "code_patterns": ["authenticate(", "isAuthenticated"],
    "file_patterns": ["*.js", "*.ts"],
    "intent": "find auth middleware implementation"
  },
  "directory": "/Users/dev/my-project"
}
```

### Response

Returns ranked code snippets with:
- File paths
- Line numbers
- Relevance scores
- Code content
- Reasoning for each match

## Usage Examples

Ask your AI assistant to search code naturally:

```
"Use greb mcp to find authentication middleware"
"Use greb mcp to find all API endpoints"
"Use greb mcp to look for database connection setup"
"Use greb mcp to find where user validation happens"
"Use greb mcp to search for error handling patterns"
```

## Links

- [Website](https://grebmcp.com)
- [Documentation](https://grebmcp.com/docs)
- [Get API Key](https://grebmcp.com/dashboard/api-keys)

## License

MIT
