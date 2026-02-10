# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.0] - 2026-02-06

### Added

- **Core CLI Framework**: Command-line interface built with `clap` featuring subcommands, global options, and configuration management
- **Agent Loop**: Core agentic orchestration with streaming responses, tool execution, and conversation management
- **Tool System**: Comprehensive filesystem and shell tools including:
  - `read_file` - Read file contents with line offset and limit
  - `write_file` - Write or overwrite files with diff preview
  - `edit_file` - Line-based file editing
  - `glob` - File pattern matching with `globset`
  - `grep` - Content search using the `grep` crate
  - `bash` - Shell command execution with timeout and dangerous pattern detection
  - `list_directory` - Directory listing with hidden file support
- **AI Provider Support**: Multi-provider architecture supporting:
  - Anthropic (Claude 3/4 family with extended thinking)
  - OpenAI-compatible APIs (OpenAI, Azure, custom endpoints)
  - Ollama (local models via OpenAI-compatible interface)
  - Smart provider auto-detection from environment variables
- **Symbol Index**: Code navigation system featuring:
  - Tree-sitter based parsing for TypeScript, JavaScript, Rust, Python, and Go
  - SQLite-backed symbol database with fuzzy search
  - Background indexing with parallel file processing
  - Usage detection and dependency tracking
- **RAG System**: Retrieval-Augmented Generation with:
  - Semantic code chunking for multiple languages
  - SQLite-based vector store with cosine similarity
  - OpenAI and Ollama embedding providers with LRU caching
  - Incremental background indexing
- **Session Management**: Persistent conversation storage:
  - SQLite persistence with WAL mode
  - Session save/load with metadata
  - Todo/task tracking within sessions
  - Working set management for context windowing
- **Terminal UI**: Production-grade TUI built with `ratatui` and `crossterm`:
  - Real-time streaming markdown rendering
  - Slash command system (/help, /clear, /exit, /model, /session, /compact, /status)
  - Tool confirmation dialogs with diff preview
  - Session status bar integration
  - History navigation with arrow keys
- **MCP Protocol**: Model Context Protocol support for extensible tools:
  - JSON-RPC over stdio transport
  - Connection management and lifecycle handling
  - Tool wrapper integration with existing tool system
- **LSP Integration**: Language Server Protocol client:
  - Document synchronization and diagnostics caching
  - Hover, definition, and references support
  - Per-language configuration for 9+ languages
  - File scoping by extension and root markers
- **Security Features**:
  - Dangerous pattern detection for shell commands
  - Path traversal prevention
  - Tool approval system with user confirmation
  - Audit logging for all operations
- **Configuration**: Hierarchical config system supporting `.codi.json` with:
  - Provider and model selection
  - Auto-approval settings for safe tools
  - Custom dangerous patterns
  - System prompt additions
- **Telemetry and Metrics**: Comprehensive instrumentation:
  - Operation timing with spans
  - Token and cost tracking per request
  - Criterion-based benchmarks for all major components
- **Cross-Platform Support**: 
  - Unix and Windows compatibility
  - Cross-platform IPC abstractions for future multi-agent support
  - Proper path handling for all operating systems

### Changed

- Initial Rust implementation providing significant performance improvements over TypeScript baseline
- Memory-efficient streaming responses with token counting
- SQLite-based persistence replacing JSON file storage

### Security

- Implemented path traversal validation preventing access outside project directory
- Added dangerous command pattern detection for bash operations
- Established secure defaults requiring user confirmation for destructive operations
- Comprehensive audit logging for security-sensitive operations

[Unreleased]: https://github.com/anomalyco/codi-rs/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/anomalyco/codi-rs/releases/tag/v0.1.0
