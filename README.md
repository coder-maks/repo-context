# repo-context

Generate repository context for AI consumption.

## Features

- ✅ Respects `.gitignore` automatically
- ✅ Supports `.repoignore` for additional exclusions
- ✅ CLI flag `-e` for one-off exclusions
- ✅ Excludes `.git` directory
- ✅ Generates file tree with emojis
- ✅ Wraps file contents in `<file>` tags
- ✅ Cross-platform (Linux, Windows, macOS)

## Installation

Download the binary for your platform from [Releases](https://github.com/coder-maks/repo-context/releases):

- **Linux**: `repo-context-linux-x86_64`
- **Windows**: `repo-context-windows-x86_64.exe`
- **macOS (Intel)**: `repo-context-macos-x86_64`
- **macOS (Apple Silicon)**: `repo-context-macos-arm64`

### Linux/macOS:
```bash
# Download
curl -L https://github.com/coder-maks/repo-context/releases/latest/download/repo-context-linux-x86_64 -o repo-context

# Make executable
chmod +x repo-context

# Run
./repo-context
```

### Windows:
Download `repo-context-windows-x86_64.exe` and run in terminal.

## Usage

```bash
# Generate context.md with default settings
./repo-context

# Specify output file
./repo-context --output my-context.md

# Tree only (no file contents)
./repo-context --tree-only

# Exclude additional patterns (comma-separated)
./repo-context -e "*.png,*.jpg,target/"

# Combine .repoignore + CLI exclusions
./repo-context -e "temp/,*.tmp"

# Show help
./repo-context --help
```

## Exclusion Priority

The tool combines exclusions from multiple sources:

1. **`.gitignore`** - Always respected (built-in Git ignore patterns)
2. **`.repoignore`** - Project-specific exclusions (optional)
3. **`-e` flag** - One-off exclusions for specific runs

### Example `.repoignore` file:

```
# repo-context ignore file
# Syntax same as .gitignore

# Build artifacts
target/
*.exe

# IDE files
.vscode/
.idea/

# Large assets
assets/textures/*.png
*.zip
```

## How it works

1. Walks through your repository
2. Applies exclusion rules from `.gitignore`, `.repoignore`, and `-e` flag
3. Generates a markdown file with:
   - File tree structure
   - Contents of each file wrapped in `<file path="...">` tags

Perfect for feeding repository context to AI assistants!

## Examples

### Basic usage (respects .gitignore only):
```bash
./repo-context
```

### With .repoignore file:
Create `.repoignore` in your repo root, then:
```bash
./repo-context
```

### One-off exclusions:
```bash
./repo-context -e "*.md,docs/"
```

### Complex scenario:
```bash
# Exclude heavy files for AI context
./repo-context -e "*.png,*.jpg,*.mp4,assets/,dist/" --output ai-context.md
```

## License

MIT - see [LICENSE](LICENSE) file