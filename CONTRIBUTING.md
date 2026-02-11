# Contributing to Codi (Rust)

We welcome contributions! Whether you're fixing bugs, adding features, or improving documentation, your help is appreciated.

## Getting Started

### Prerequisites

- Rust 1.85 or later
- Cargo (comes with Rust)

### Setup

```bash
# Clone and enter the repo
git clone https://github.com/laynepenney/codi-rs.git
cd codi-rs

# Build the project
cargo build

# Run tests
cargo test
```

## Development Workflow

```bash
# Run in development mode
cargo run

# Run tests
cargo test

# Run tests with output
cargo test -- --nocapture

# Run specific test
cargo test test_name

# Build for production
cargo build --release

# Run benchmarks
cargo bench

# Check code formatting
cargo fmt

# Run linter
cargo clippy
```

## Making Changes

> **IMPORTANT**: Never push directly to main. Always use feature/bugfix branches and pull requests.

1. **Fork the repository** and clone your fork
2. **Create a feature branch**: `git checkout -b feat/amazing-feature` (or `fix/`, `chore/`)
3. **Make your changes** following the coding guidelines below
4. **Run tests**: `cargo test`
5. **Run linter**: `cargo clippy`
6. **Format code**: `cargo fmt`
7. **Commit your changes**: `git commit -m 'feat: add amazing feature'`
8. **Push to your fork**: `git push -u origin feat/amazing-feature`
9. **Open a Pull Request**: `gh pr create` or via GitHub UI

### Branch Naming Convention

- `feat/` - New features
- `fix/` - Bug fixes
- `chore/` - Maintenance, refactoring, documentation updates
- `docs/` - Documentation-only changes

## Coding Guidelines

### Code Style

- **Rust**: Follow standard Rust conventions (snake_case for functions/variables, PascalCase for types)
- **Error Handling**: Use `anyhow` for application errors, `thiserror` for library errors
- **Async**: Use `tokio` for async runtime, `async-trait` for async traits
- **Formatting**: Run `cargo fmt` before committing
- **Linting**: Address all `cargo clippy` warnings

### Commit Messages

We follow [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` - New features
- `fix:` - Bug fixes
- `docs:` - Documentation changes
- `refactor:` - Code refactoring
- `test:` - Adding or updating tests
- `chore:` - Maintenance tasks
- `perf:` - Performance improvements

#### Commit Message Format

Every commit should include a `Wingman:` trailer to track Codi's assistance:

```bash
git commit -m "feat: add amazing feature

This adds the amazing feature for user productivity.

Wingman: Codi <codi@layne.pro>"
```

According to Git conventions, trailers should be placed at the end of the commit message body, after a blank line.

#### Collaborative Work (Co-authored-by)

When multiple people (humans or AI) contribute to a commit, use `Co-authored-by:` trailers:

```bash
git commit -m "feat: authentication system

Implement OAuth2 authentication with Google and GitHub providers.

Co-authored-by: Alice <alice@example.com>
Co-authored-by: Bob <bob@example.com>
Co-authored-by: Codi <codi@layne.pro>
Wingman: Codi <codi@layne.pro>"
```

Best practices for multi-author commits:
- Order: Human collaborators first, then other
- Format: `Co-authored-by: Name <email>`
- Required: Always include `Wingman: Codi <codi@layne.pro>` if Codi assisted

## Testing

- Tests are in `tests/` and inline with `#[cfg(test)]`
- Run all tests: `cargo test`
- Run specific test: `cargo test test_name`
- Run with output: `cargo test -- --nocapture`
- Run TUI snapshot tests: `cargo test --test tui_exec_cell`
- Optional snapshot update workflow:
  - `cargo install cargo-insta`
  - `cargo insta test --test tui_exec_cell`
  - `cargo insta accept`

### Benchmarks

Performance tests are in `benches/`:

```bash
cargo bench
```

## Documentation

- Update `README.md` for user-facing changes
- Update `docs/` for architectural or design documentation
- Add inline rustdoc comments for public functions and types
- Follow Rust documentation best practices

## License & Contributor Agreement

Codi is dual-licensed under AGPL-3.0 (open source) and a commercial license. See [LICENSING.md](./LICENSING.md) for details.

By contributing to Codi, you agree that:

1. Your contributions will be licensed under the same dual-license terms (AGPL-3.0 / Commercial)
2. You have the right to submit the contribution under these terms
3. You grant the project maintainers the right to use your contribution in both open source and commercial versions

For significant contributions (new features, major refactors), we may ask you to sign a Contributor License Agreement (CLA) to ensure we can continue offering commercial licenses.

## Questions?

Feel free to open an issue for any questions or suggestions!
