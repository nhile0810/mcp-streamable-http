# MCP Servers over Streamable HTTP — Step-by-Step Guide

📝 **Read the full article here**: [MCP Servers over Streamable HTTP (Step-by-Step)](https://aibootcamp.dev/blog/remote-mcp-servers)


---

This repository contains a complete, working example of how to build and run an **MCP (Model Context Protocol) server** using Python, `mcp`, and `FastAPI`. You’ll learn how to:

- Expose tools and functions over HTTP using the MCP protocol
- Connect those tools to AI assistants like [Cursor](https://cursor.com/)
- Use streamable HTTP as the transport
- Mount multiple MCP servers in a FastAPI app

---

## 📁 Folder Structure

```bash
.
├── docs/                        # Diagrams and assets (e.g., mcp-client-server.png)
├── fastapi_example/            # Example mounting multiple MCP servers in FastAPI
│   ├── echo_server.py          # A server exposing a simple echo tool
│   ├── math_server.py          # A server exposing a math tool
│   └── server.py               # FastAPI app that mounts both echo and math servers
├── .gitignore
├── .python-version             # Python version (for tools like pyenv or uv)
├── pyproject.toml              # Project config and dependencies
├── readme.md                   # You're here!
├── runtime.txt                 # Python runtime for platforms like Render
├── server.py                   # Basic standalone MCP server using Tavily search
├── uv.lock                     # Lockfile for uv dependency manager
```

⸻

🛠 Quickstart
1.	Install uv (recommended Python package manager)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

2.	Install dependencies and set up environment

```
uv venv && source .venv/bin/activate
uv pip install -r pyproject.toml
```

3.	Run the basic MCP server
This uses the Tavily API to expose a simple web_search tool.

```
uv run server.py
```

4.	Run the FastAPI app with multiple MCP servers

```
uv run fastapi_example/server.py
```

This will mount:
- http://localhost:8000/echo/mcp/
- http://localhost:8000/math/mcp/

⸻

🧪 Debug with MCP Inspector
1.	Install CLI support

```bash
uv add 'mcp[cli]'
```

2.	Launch the inspector

```
uv run mcp dev server.py
```

Then go to: `http://localhost:6274/?MCP_PROXY_AUTH_TOKEN=...`



⸻

🔌 Connect to Cursor

In Cursor, add your MCP server under Chat Settings > MCP Servers:
```json
{
  "mcpServers": {
    "tavily": {
      "url": "http://localhost:8000/mcp/"
    }
  }
}
```

✅ Note: You must include the trailing / in the URL.

⸻
