# MCP Research Chatbot

An intelligent chatbot powered by the Model Context Protocol (MCP) that enables natural language interaction with academic research papers. This project demonstrates advanced LLM integration using multiple MCP servers for research paper discovery, local storage, and conversational AI.

## 🚀 Features

- **Smart Paper Discovery**: Search arXiv papers by topic using natural language
- **Local Paper Management**: Store and organize research papers locally with metadata
- **Multi-Server Architecture**: Integrate filesystem, research, and web fetch capabilities
- **Conversational Interface**: Chat with papers using Groq's LLM integration
- **Dynamic Tool Calling**: Automatic tool selection and execution based on user queries
- **Resource Management**: Browse topics and papers using URI-based resource system
- **Prompt Templates**: Pre-built prompts for comprehensive research analysis

## 🏗️ Architecture

The project consists of several key components:

### Core Components
- **`mcp_chatbot.py`**: Main chatbot client with Groq LLM integration
- **`research_server.py`**: Custom MCP server for arXiv paper search and management
- **`server_config.json`**: Configuration for multiple MCP servers

### MCP Servers
1. **Research Server**: Custom server for academic paper operations
2. **Filesystem Server**: File system access and management
3. **Fetch Server**: Web content retrieval capabilities

### Data Storage
- **`papers/`**: Organized storage of paper metadata by topic
- Local JSON files store paper information, summaries, and metadata

## 📋 Prerequisites

- Python 3.10 or higher
- Node.js (for filesystem MCP server)
- UV package manager
- Groq API key

## 🛠️ Installation

1. **Clone the repository**:
```bash
git clone <repository-url>
cd mcp_project
```

2. **Install dependencies**:
```bash
uv sync
```

3. **Set up environment variables**:
Create a `.env` file in the project root:
```env
GROQ_API_KEY=your_groq_api_key_here
```

4. **Install Node.js dependencies** (for filesystem server):
```bash
npm install -g @modelcontextprotocol/server-filesystem
```

## 🚀 Usage

### Starting the Chatbot

```bash
uv run mcp_chatbot.py
```

### Basic Commands

#### Search and Resource Access
- **Search papers**: `search for machine learning papers`
- **Browse topics**: `@folders` - Lists all available research topics
- **Access topic papers**: `@ai_interpretability` - Shows papers in specific topic
- **Natural queries**: `What are the latest trends in transformer architecture?`

#### Prompt System
- **List prompts**: `/prompts` - Shows available prompt templates
- **Execute prompt**: `/prompt generate_search_prompt topic=quantum_computing num_papers=10`

### Example Interaction

```
Query: search for papers on AI interpretability

# Chatbot searches arXiv, stores papers locally, and provides summaries

Query: @folders
# Shows: ai_interpretability, llm_reasoning, transformer

Query: @ai_interpretability  
# Displays detailed information about stored papers in that topic

Query: What are the main themes in AI interpretability research?
# Uses stored papers to provide comprehensive analysis
```

## 🔧 Configuration

### Server Configuration (`server_config.json`)

```json
{
    "mcpServers": {
        "filesystem": {
            "command": "npx",
            "args": ["-y", "@modelcontextprotocol/server-filesystem", "."]
        },
        "research": {
            "command": "uv",
            "args": ["run", "research_server.py"]
        },
        "fetch": {
            "command": "uvx",
            "args": ["mcp-server-fetch"]
        }
    }
}
```

## 🛠️ Available Tools

### Research Server Tools

1. **`search_papers(topic, max_results)`**
   - Search arXiv for papers on specified topic
   - Store results locally with metadata
   - Returns list of paper IDs

2. **`get_paper_info(paper_id)`**
   - Retrieve detailed information for specific paper
   - Returns formatted JSON with title, authors, summary, etc.

### Resources

- **`papers://folders`**: List all available research topics
- **`papers://{topic}`**: Get detailed papers for specific topic

### Prompts

- **`generate_search_prompt(topic, num_papers)`**: Create comprehensive research analysis prompt

## 📁 Project Structure

```
mcp_project/
├── mcp_chatbot.py          # Main chatbot client
├── research_server.py      # Custom MCP research server
├── server_config.json      # MCP server configurations
├── pyproject.toml         # Project dependencies
├── .env                   # Environment variables (create this)
├── papers/                # Local paper storage
│   ├── ai_interpretability/
│   ├── llm_reasoning/
│   └── transformer/
└── README.md              # This file
```

## 🔄 How It Works

1. **Server Connection**: Chatbot connects to multiple MCP servers on startup
2. **Tool Discovery**: Automatically discovers available tools and resources
3. **Query Processing**: User queries are processed by Groq LLM with tool calling
4. **Tool Execution**: Relevant tools are called automatically based on query intent
5. **Response Generation**: Results are integrated and presented conversationally

## 🧩 Extending the Project

### Adding New Tools

Extend `research_server.py` with new `@mcp.tool()` functions:

```python
@mcp.tool()
def analyze_paper_citations(paper_id: str) -> str:
    """Analyze citation patterns for a specific paper."""
    # Implementation here
    pass
```

### Adding New Resources

Create new resource endpoints:

```python
@mcp.resource("papers://trending/{timeframe}")
def get_trending_papers(timeframe: str) -> str:
    """Get trending papers in specified timeframe."""
    # Implementation here
    pass
```

### Adding New Servers

1. Add server configuration to `server_config.json`
2. Update `connect_to_servers()` method in `mcp_chatbot.py`

## 🤝 Dependencies

- **groq**: LLM API integration
- **arxiv**: Academic paper search
- **mcp**: Model Context Protocol framework
- **nest-asyncio**: Async event loop management
- **python-dotenv**: Environment variable management

## 📚 Use Cases

- **Academic Research**: Discover and analyze papers on specific topics
- **Literature Reviews**: Automated synthesis of research landscapes
- **Trend Analysis**: Identify patterns and gaps in research areas
- **Paper Discovery**: Natural language search of academic literature
- **Research Organization**: Local storage and categorization of papers

## 🐛 Troubleshooting

### Common Issues

1. **Server Connection Errors**: Ensure all MCP servers are properly installed
2. **API Key Issues**: Verify Groq API key is set in `.env` file
3. **Node.js Dependencies**: Install filesystem server globally with npm
4. **Port Conflicts**: Check if other processes are using required ports

### Debug Mode

Run with verbose output:
```bash
PYTHONPATH=. uv run mcp_chatbot.py --verbose
```

## 📄 License

This project is open source and available under the MIT License.

## 🚀 Future Enhancements

- Web interface for easier interaction
- Paper recommendation system
- Citation network analysis
- Multi-language paper support
- Integration with additional academic databases
- Real-time collaboration features

---

**Built with ❤️ using the Model Context Protocol and modern AI frameworks**
