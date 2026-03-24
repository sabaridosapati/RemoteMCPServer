# ExpenseTracker MCP Server

A remote MCP server built with [FastMCP](https://github.com/jlowin/fastmcp) that exposes expense tracking tools over HTTP. Designed to work with any MCP-compatible client such as Claude Desktop.

## Features

- Add expenses with category, subcategory, date, and notes
- List expenses within a date range
- Summarize expenses by category
- Exposes available categories as an MCP resource

## Tools

| Tool | Description |
|------|-------------|
| `add_expense` | Add a new expense entry |
| `list_expenses` | List all expenses within a date range |
| `summarize` | Summarize total spending by category |

## Supported Categories

`Food`, `Travel`, `Transport`, `Shopping`, `Bills`, `Healthcare`, `Education`, `Business`, `Other`

## Requirements

- Python >= 3.11
- Dependencies managed via `uv`

## Installation

```bash
uv sync
```

## Running the Server

```bash
uv run python main.py
```

The server starts on `http://0.0.0.0:8000` using HTTP transport.

## Claude Desktop Configuration

Add the following to your `claude_desktop_config.json`:

```json
"ExpenseTracker": {
  "command": "C:\\Users\\<your-user>\\.local\\bin\\uv.EXE",
  "args": [
    "run",
    "--with", "fastmcp",
    "--with", "aiosqlite",
    "fastmcp",
    "run",
    "C:\\path\\to\\Custom_Remote-mcp-server\\main.py"
  ],
  "transport": "stdio"
}
```

## Data Storage

Expenses are stored in a SQLite database at the system temp directory (`tempfile.gettempdir()/expenses.db`).
