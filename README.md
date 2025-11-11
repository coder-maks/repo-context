# repo-context

Generate repository context for AI consumption.

## Installation

Download the binary for your platform from [Releases](https://github.com/YOUR_USERNAME/repo-context/releases):

- Linux: `repo-context-linux-x86_64`
- Windows: `repo-context-windows-x86_64.exe`
- macOS (Intel): `repo-context-macos-x86_64`
- macOS (Apple Silicon): `repo-context-macos-arm64`

## Usage

```bash
# Generate context.md with default settings
./repo-context

# Specify output file
./repo-context --output my-context.md

# Tree only (no file contents)
./repo-context --tree-only
```

## Features

- ✅ Respects .gitignore automatically
- ✅ Generates file tree
- ✅ Wraps file contents in `<file>` tags
- ✅ Cross-platform (Linux, Windows, macOS)

## License

MIT