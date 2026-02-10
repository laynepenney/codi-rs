# codi-rs

**Codi** - Your AI coding wingman, reimagined in Rust.

A high-performance terminal AI assistant supporting Claude, OpenAI, Ollama, and more. Built with Rust for speed, safety, and reliability.

## Features

- 🤖 **Multi-Provider Support** - Claude, OpenAI, Ollama, and OpenAI-compatible APIs
- 🛠️ **Powerful Tool System** - File operations, shell commands, grep, glob, and more
- 🧠 **RAG System** - Semantic code search with vector embeddings
- 🔍 **Symbol Index** - Tree-sitter based code navigation
- 👥 **Multi-Agent** - Parallel workers with IPC permission bubbling
- 🖥️ **Terminal UI** - Rich ratatui-based interactive interface
- ⚡ **High Performance** - Native speed with Rust's zero-cost abstractions

## Quick Start

```bash
# Clone the repository
git clone https://github.com/laynepenney/codi-rs.git
cd codi-rs

# Build
cargo build --release

# Run
cargo run
```

## Installation

### From Source

```bash
git clone https://github.com/laynepenney/codi-rs.git
cd codi-rs
cargo install --path .
```

### Prerequisites

- Rust 1.85 or later
- At least one AI provider API key (Anthropic, OpenAI, or Ollama for local)

## Configuration

Set your API keys:

```bash
export ANTHROPIC_API_KEY=sk-ant-...
# or
export OPENAI_API_KEY=sk-...
```

Or create a `.codi.yaml` config file:

```yaml
provider: anthropic
model: claude-sonnet-4-20250514
auto_approve:
  - read_file
  - glob
  - grep
```

## Usage

```bash
# Start interactive session
codi

# Run with specific provider
codi --provider openai --model gpt-4o

# Run with local model
codi --provider ollama --model llama3.2
```

## Documentation

- [ROADMAP.md](./docs/ROADMAP.md) - Feature roadmap and architecture
- [CONTRIBUTING.md](./CONTRIBUTING.md) - How to contribute
- [SECURITY.md](./SECURITY.md) - Security policies and reporting
- [CHANGELOG.md](./CHANGELOG.md) - Version history

## Status

Core feature parity with the TypeScript CLI is complete. See `docs/ROADMAP.md` for ongoing work.

### Completed Phases

| Phase | Description | Status |
|-------|-------------|--------|
| **0** | Foundation - types, errors, config, CLI shell | ✅ Complete |
| **1** | Tool layer - file tools, grep, glob, bash | ✅ Complete |
| **2** | Provider layer - Anthropic, OpenAI, Ollama | ✅ Complete |
| **3** | Agent loop - core agentic orchestration | ✅ Complete |
| **4** | Symbol index - tree-sitter based code navigation | ✅ Complete |
| **5** | RAG system - vector search with embeddings | ✅ Complete |
| **6** | Terminal UI - ratatui based interface | ✅ Complete |
| **7** | Multi-agent - IPC-based worker orchestration | ✅ Complete |

## Features

### Providers

```rust
use codi::{anthropic, openai, ollama, create_provider_from_env};

// Auto-detect from environment
let provider = create_provider_from_env()?;

// Or use specific provider
let claude = anthropic("claude-sonnet-4-20250514")?;
let gpt = openai("gpt-4o")?;
let local = ollama("llama3.2");
```

**Supported Providers:**
- **Anthropic** - Full Claude API with streaming, tool use, vision
- **OpenAI** - GPT models with streaming and tool use  
- **Ollama** - Local models, no API key required
- **Any OpenAI-compatible API** - Azure, Together, Groq, etc.

### Agent Loop

```rust
use codi::agent::{Agent, AgentConfig, AgentOptions};
use codi::tools::ToolRegistry;
use std::sync::Arc;

let provider = anthropic("claude-sonnet-4-20250514")?;
let registry = Arc::new(ToolRegistry::with_defaults());

let mut agent = Agent::new(AgentOptions {
    provider,
    tool_registry: registry,
    system_prompt: Some("You are a helpful assistant.".to_string()),
    config: AgentConfig::default(),
    callbacks: Some(callbacks),
});

// Chat with streaming
agent.chat("Hello!", |chunk| {
    print!("{}", chunk);
}).await?;
```

### Tools

Built-in tools include:
- `read_file` - Read file contents
- `write_file` - Write or overwrite files
- `edit_file` - Edit files with search/replace
- `glob` - Find files by pattern
- `grep` - Search file contents
- `bash` - Execute shell commands
- `list_directory` - Browse directories
- `rag_search` - Semantic code search
- `symbol_index` - Find and navigate code symbols

### Terminal UI

Full ratatui-based interface with:
- Session management
- Streaming responses
- File browser with preview
- Command palette
- Git integration
- Diff viewer

## Development

```bash
# Run tests
cargo test

# Run benchmarks
cargo bench

# Build for production
cargo build --release

# Run linter
cargo clippy

# Format code
cargo fmt
```

See [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed contribution guidelines.

## License

Codi is dual-licensed under:

- **AGPL-3.0** - Open source license (see [LICENSE](./LICENSE))
- **Commercial License** - For proprietary use (see [LICENSING.md](./LICENSING.md))

## Security

For security issues, please email [security@layne.pro](mailto:security@layne.pro) instead of using the issue tracker.

See [SECURITY.md](./SECURITY.md) for more details.

## Community

- GitHub Issues: https://github.com/laynepenney/codi-rs/issues
- Discussions: https://github.com/laynepenney/codi-rs/discussions

---

**Built with ❤️ and 🦀 in Rust**
